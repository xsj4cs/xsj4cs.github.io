title: java爬虫
tags: "java"
---
``` java
import java.net.*;
import java.io.*;
import java.util.regex.*;
import java.util.*;
//import java.util.Queue;
//import java.util.LinkedList;

public class Spider {
    public static void main(String args[]) throws Exception {
        getMail();
    }

    public static void getMail() throws Exception {
        URL url = new URL("http://tieba.baidu.com/p/3856188322");
        Queue<URL> q = new LinkedList<URL>();
        HashMap hm = new HashMap();
        hm.put(url, 1);
        q.add(url);
        while ((url = q.poll()) != null) {
            try {
                URLConnection con = url.openConnection();
                BufferedReader bufin = new BufferedReader(
                        new InputStreamReader(con.getInputStream()));
            } catch (Exception e) {
                continue;
            }
            URLConnection con = url.openConnection();
            BufferedReader bufin = new BufferedReader(new InputStreamReader(
                    con.getInputStream()));
            String line = null;
            String mailreg = "\\w+@\\w+[\\.\\w+]+";
            String urlreg = "http.*?\"";
            Pattern p = Pattern.compile(mailreg);
            Pattern purl = Pattern.compile(urlreg);
            while ((line = bufin.readLine()) != null) {
                Matcher m = p.matcher(line);
                Matcher murl = purl.matcher(line);
                while (m.find()) {
                    System.out.println(m.group());
                }
                while (murl.find()) {
                    String tmp = murl.group().toString();
                    tmp = tmp.replaceAll("\"", "");
                    boolean flag = false;
                    try {
                        URL ttmp = new URL(tmp);
                    } catch (Exception e) {
                        flag = true;
                        continue;
                    }
                    URL ttmp = new URL(tmp);
                    if(!hm.containsKey(ttmp))
                        q.add(ttmp);
                    //System.out.println(tmp);
                }

            }
        }
    }
}

```
