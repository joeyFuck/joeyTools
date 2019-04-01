### 1. 一般处理程序设置文件直接url下载限制
```
<configuration>
    <system.webServer> 
      <handlers>
        <add name="DownloadHandler" path="*.xls" verb="*" type="WebApplication1.DownloadHandler"/>
      </handlers>
    </system.webServer>
</configuration>
```
```
public class DownloadHandler : IHttpHandler
{
    public DownloadHandler(){}
    /// <summary>
    /// 指示IHttpHandler 实例是否可再次使用
    /// </summary>
    public bool IsReusable
    {
        get { return true; }
    }
    public void ProcessRequest(HttpContext context)
    {
            Uri referrerUri = HttpContext.Current.Request.UrlReferrer;//获取下载之前访问的那个页面的uri
            Uri currentUri = HttpContext.Current.Request.Url;  
            if (referrerUri == null)//没有前导页，直接访问下载页
            {
                //输出提示，可以根据自身要求完善此处代码
                HttpContext.Current.Response.Write("请不要盗链本站资源，请从首页访问。<a href='../index.aspx'>进入首页</a>");
                return;
            }
            else
            {
                string file = context.Server.MapPath(context.Request.FilePath);
                string sFileName = file;
                FileStream fileStream = new FileStream(sFileName, FileMode.Open);
                long fileSize = fileStream.Length;
                byte[] fileBuffer = new byte[fileSize];
                fileStream.Read(fileBuffer, 0, (int)fileSize);
                //如果不写fileStream.Close()语句，用户在下载过程中选择取消，将不能再次下载
                fileStream.Close();

                context.Response.ContentType = "application/file";
                var fileNameArr = context.Request.FilePath.Split('/');
                context.Response.AppendHeader("Content-Disposition", "attachment;filename=" + fileNameArr[fileNameArr.Length - 1]);
                context.Response.AddHeader("Content-Length", fileSize.ToString());

                context.Response.BinaryWrite(fileBuffer);
                context.Response.End();
                context.Response.Close();
            }
    }
}
```
