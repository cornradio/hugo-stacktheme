+++

title = "保存object到xml"
date = "2021-06-01"
author = "kasusa"
cover = ""
tags = ["csharp"]
description = "使用到了datacontract"
showFullContent = false

+++



## 对实体类做标记

` [DataContract]` 标记在class前。

` [DataMember]` 标记在需要保存的属性前。

```cs
 [DataContract]
public class Car
{
  [DataMember]
  public string name;

  [DataMember]
  double power;

  [DataMember]
  List<Wheel> wheels;
}
```



## 拷贝这两个函数

保存：保存文件到xml，文件目录和程序目录相同，文件名自定。

读取：从指定文件名读取。

```cs
static void SaveViaDataContractSerialization<T>(T serializableObject, string filepath)
{
  var serializer = new DataContractSerializer(typeof(T));
  var settings = new XmlWriterSettings()
  {
    Indent = true,
    IndentChars = "\t",
  };
  var writer = XmlWriter.Create(filepath, settings);
  serializer.WriteObject(writer, serializableObject);
  writer.Close();
}


static T LoadViaDataContractSerialization<T>(string filepath)
{
  var fileStream = new FileStream(filepath, FileMode.Open);
  var reader = XmlDictionaryReader.CreateTextReader(fileStream, new XmlDictionaryReaderQuotas());
  var serializer = new DataContractSerializer(typeof(T));
  T serializableObject = (T)serializer.ReadObject(reader, true);
  reader.Close();
  fileStream.Close();
  return serializableObject;
}
```



## 读取方法

使用上面两个方法来读取和存储

```csharp
// Save single object
Car bmw = new Car("BMW", 200, new List<string> { "Left", "Right" });    // create object
SaveViaDataContractSerialization(bmw, "bmw.xml");                       // save object
bmw = null;                                                             // delete object
bmw = LoadViaDataContractSerialization<Car>("bmw.xml");                 // reload object
Console.WriteLine(bmw.ToString());                                      // print object


// Save list of objects
List<Car> carList = new List<Car>                                       // create object list
{
new Car("Porsche", 250, new List<string> { "Left" }),
new Car("Mercedes", 150, new List<string> { "Front", "Back" }),
new Car("Aston Martin", 300, new List<string> { "Front" })
};
SaveViaDataContractSerialization(carList, "cars.xml");                  // save object list
carList = null;                                                         // delete object list
carList = LoadViaDataContractSerialization<List<Car>>("cars.xml");      // reload object list
foreach (var a in carList)                                              // print object list
Console.WriteLine(a.ToString());

Console.ReadLine();
```



原视频：[https://www.youtube.com/watch?v=GzZu3eYDBmM](https://www.youtube.com/watch?v=GzZu3eYDBmM)

demo代码：[https://pastebin.com/mRTmdiK5](https://pastebin.com/mRTmdiK5)

