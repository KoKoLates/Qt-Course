# file I/O
## main include
```cpp
#include <QfileDialog>
#include <QFile>
#include <QTextStream> //for text file
#include <QImage> //for image file
```
## filePath
Get the path of existed file by storing it as a QString data. And ones can then operate I/O of such file
```cpp
QString filePath = QFileDialog::getOpenFileName(this,tr("OpenText"),"",tr("Text(*.txt *.csv)"));
QString filePath = QFileDialog::getOpenFileName(this,tr("OpenImage"),"",tr("Image(*.png *.jpg *.jepg)"));
QString filePath = "Path"; // directlt indicate the file path
```
## Text file
### File Read
Read the file indicated by filePath.<br>
The defalt of unicode is UTF-8, as any file using other form will get corrupt
```cpp
QFile fileRead(filePath); 
if(fileRead.open(QIODevice::ReadOnly)){
  QTextStream input(&fileRead);  
  input.setCodec("UTF-8");
  while(!input.atEnd()){
    QString line = input.readline();
    ui->textBrowser->append(line.toStdString().c_str());
  }
  fileRead.close();
}
```
### File Write
Write the text file
```cpp
QString UserInput = ui->lineEdit->text(); 
//or use other ways to get the output QString

QFile fileWrite(filePath);
if(fileWrite.open(QIODevice::WriteOnly | QIODevice::Append | QIODevice::Text )){
  QTextStream output(&fileWrite);
  output<<UserInput<<Qt::endl;
  fileWrite.close();
}
```
## Image file
### Read and show in the label
```cpp
QPixmap icon("imagePath");
ui->label->setPixmap(icon.scaled(ui->label->width(),ui->label->height(),Qt::KeepAspectRatio));
```