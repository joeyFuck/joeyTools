using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleAppHttpClient
{
    class Program
    {
        static void Main(string[] args)
        {
            var resGet = TestGet();
            Console.WriteLine(resGet.Result);

            var resPost = TestPostAsync();
            Console.WriteLine(resPost.Result);

            Console.WriteLine("Hit enter to exit...");
            Console.ReadLine();
        }

        /// <summary>
        /// async HttpClient Get
        /// </summary>
        /// <returns></returns>
        static async Task<string> TestGet()
        {
            string Uri = "http://localhost:5008/Home/Get?id=123";
            HttpClient httpClient = new HttpClient();

            // 创建一个异步GET请求，当请求返回时继续处理（Continue-With模式）
            HttpResponseMessage response = await httpClient.GetAsync(Uri);
            response.EnsureSuccessStatusCode();
            string resultStr = await response.Content.ReadAsStringAsync();
            return resultStr;
        }


        public static async Task<string> TestPostAsync()
        {
            using (HttpClient httpClient = new HttpClient())
            {
                // 设置请求头信息
                httpClient.DefaultRequestHeaders.Add("Host", "localhost:5008");
                httpClient.DefaultRequestHeaders.Add("Method", "Post");
                httpClient.DefaultRequestHeaders.Add("KeepAlive", "false");   // HTTP KeepAlive设为false，防止HTTP连接保持
                httpClient.DefaultRequestHeaders.Add("UserAgent",
                    "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.95 Safari/537.11");

                // 构造POST参数
                HttpContent postContent = new FormUrlEncodedContent(new Dictionary<string, string>()
                   {
                      {"id", "123456"},
                      {"name","joey"},
                      {"o_code","789456" },
                      {"o_type","666" },
                   });

                HttpResponseMessage response = await httpClient.PostAsync("http://localhost:5008/Home/Post", postContent);

                response.EnsureSuccessStatusCode();
                string resultStr = await response.Content.ReadAsStringAsync();

                Console.WriteLine("响应是否成功：" + response.IsSuccessStatusCode);

                Console.WriteLine("响应头信息如下：\n");
                var headers = response.Headers;
                foreach (var header in headers)
                {
                    Console.WriteLine("{0}: {1}", header.Key, string.Join("", header.Value.ToList()));
                }

                return resultStr;
            } 
        }

    }
}
