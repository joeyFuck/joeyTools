1. 查看端口占用 
   netstat -ano

2. 通过pid找到进程信息
   tasklist|findstr "2396"

3. 通过pid kill进程
    taskkill/pid 2396

4. 列出当前文件夹下所有文件(不列出目录)
   DIR /S/B/a-d>列表.TXT
   保存为.bat
    
