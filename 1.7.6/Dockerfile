FROM microsoft/windowsservercore

ENV JAVA_HOME c:\\Java\\jre1.8.0_91

RUN mkdir c:\temp
RUN powershell (new-object System.Net.WebClient).Downloadfile('http://javadl.oracle.com/webapps/download/AutoDL?BundleId=210185', 'C:\temp\jre-8u91-windows-x64.exe')
RUN powershell Start-Process -FilePath C:\temp\jre-8u91-windows-x64.exe -PassThru -Wait -ArgumentList "/s,INSTALLDIR=c:\Java\jre1.8.0_91,/L,install64.log"
RUN del C:\temp\jre-8u91-windows-x64.exe

RUN powershell (new-object System.Net.WebClient).Downloadfile('https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.6.zip', 'C:\temp\elasticsearch-1.7.6.zip')
RUN powershell Expand-Archive -Path c:\temp\elasticsearch-1.7.6.zip -DestinationPath c:\services\ -Force;
RUN del C:\temp\elasticsearch-1.7.6.zip

RUN c:\services\elasticsearch-1.7.6\bin\plugin.bat install mobz/elasticsearch-head

EXPOSE 9200 9300
VOLUME c:\\services\\elasticsearch-1.7.6\\config
VOLUME c:\\services\\elasticsearch-1.7.6\\data

CMD [ "c:\\services\\elasticsearch-1.7.6\\bin\\elasticsearch.bat"]