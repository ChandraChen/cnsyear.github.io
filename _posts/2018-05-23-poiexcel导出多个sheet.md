---
title: POI导出多个sheet
description: POI导出多个sheet
categories:
 - POI
tags:
 - POI
---

> POIExcel导出多个sheet

```

/**给List存值*/  
List result = new ArrayList();  
result.add(1);
result.add(1);
result.add(1);
result.add(1);
result.add(1);
String fileName = "d:\\测试.xls";  
//首先要使用Workbook类的工厂方法创建一个可写入的工作薄(Workbook)对象        
WritableWorkbook wwb = Workbook.createWorkbook(new File(fileName));  
File xlsFile = new File(fileName);  
if (!xlsFile.exists() || xlsFile.isDirectory()) {  
	xlsFile.createNewFile();  
}  
int totle = result.size();//获取List集合的size  
int mus = 2;//每个工作表格最多存储2条数据（注：excel表格一个工作表可以存储65536条）  
int avg = totle / mus;  
for (int i = 0; i < avg + 1; i++) {  
    WritableSheet ws = wwb.createSheet("列表" + (i + 1), i);  //创建一个可写入的工作表    
    //添加表头  
    ws.addCell(new Label(0, 0, "序号"));   
    ws.addCell(new Label(1, 0, "姓名"));  
    int num = i * mus;   
    int index = 0;   
    for (int m = num; m < result.size(); m++) {  
        if (index == mus) {//判断index == mus的时候跳出当前for循环  
            break;  
        }  
		//将生成的单元格添加到工作表中   
		//（这里需要注意的是，在Excel中，第一个参数表示列，第二个表示行）       
        ws.addCell(new Label(0, index + 1, result.get(i).toString()));  
        ws.addCell(new Label(1, index + 1, result.get(i).toString()));  
        index++;  
    }  
}  
wwb.write();//从内存中写入文件中     
wwb.close();//关闭资源，释放内存
// 1.设置文件ContentType类型，这样设置，会自动判断下载文件类型
response.setContentType("application/pdf");
// 清除首部的空白行。
response.reset();
response.setHeader("Cache-Control", "max-age=0");
fileName = URLEncoder.encode(fileName, "UTF-8");
// 通知浏览器下载文件而不是打开
response.setHeader("Content-Disposition", new StringBuffer(
					"attachment; filename=").append(fileName).toString());
response.setCharacterEncoding("UTF-8"); 

OutputStream fos = response.getOutputStream();
fos.write(xlsFile);
fos.close();
```

*标记：愿以千金博你巧笑，一个回眸就能让我赴汤蹈火知道不知道？鹊桥相会以不重要，只求抛弃乱世繁华倾尽一生与子偕老。
——花香蘑菇 《君临臣下》*