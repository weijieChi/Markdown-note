# 檔案目錄權限表示

首先來看 Linux 基本檔案權限結構

```
$ ls -l /tmp/myfile ←用 ls -l 列出冗長檔案資訊
-rw-rw-r-- 1 aaa aaa 11 2011-10-10 10:10 myfile ←紅字標記的為 user,綠字標記的為 group
```


## 檔案 rwx 的意思
 * r(): 可查看該檔案的內容,如可用 cat 或 less 或其他工具來閱讀。
 * w(): 可變更其內容,如可用 vi 或累加重定向來變更檔案的內容。
 * x(): 如為執行檔則可被執行,但如是 shell script 額外還要有讀的權限才可被執行(因 shell 要讀取該檔)。

## 目錄 rwx 的意思

 * r(): 列出目錄內的檔案或其子目錄(如用 ls 可顯示目錄內的檔案但並非可用 cat 來讀取目錄內的檔案)
 * w(): 增減或更名目錄內的檔案(如可對目錄內的檔案操作 rm 或 cp 或 mv 等)
 * x(): 進入目錄或執行目錄內的程式(如可 cd 進入目錄)

 ---

 # 參考
 * https://www.hy-star.com.tw/tech/linux/permission/permission.html