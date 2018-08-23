# notes
## GFW
> tracert
## port

> netstat -na | findstr "port"

>> -n或--numeric 直接使用IP地址，而不通过域名服务器。

>> -a或--all 显示所有连线中的Socket。
## stat all port-states
> [netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'](http://blog.51cto.com/stephenzhao/658587)


## goroot
> mklink \d <DIR_UNDER_$GOPATH>  <REAL_DIR>
