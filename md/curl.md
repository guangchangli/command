### curl

1. 访问

   ```
   curl url
   ```

2. 下载页面

   ```
   curl url>page.html
   ```

3. porxy

   ```
   curl -x proxy.url:port -o page.html url
   ```

4. cookies

   ```
   curl -x proxy:port -o page.html -D cookies.txt url
   ```

5. -v 显示通信过程

   ```
   curl -v url 
   curl --trace output.txt url
   curl --trace-ascii output.txt url
   ```

6. get

   ```
   curl url?params  多个get url 直接写
   ```

7. post

   ```
   curl -H "Accept: application/json" -H "Content-type: application/json"
   -X POST -d '{"xx":"xx"}' interfaceURl
   ```

   