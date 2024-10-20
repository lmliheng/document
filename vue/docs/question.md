## FAQ

在Vue文件中提示`Parsing error: No Babel config file detected for xxx`
解决方案:
在新建完Vue项目后代码第一行总是爆红很烦，想要将它清除掉，
找到项目中的`package.json`文件,按照下图指示添加`"requireConfigFile" : false`