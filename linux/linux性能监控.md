1. top

2. serverAgent配合jemeter

3. export fileName=log-con-`date`.log
    touch $fileName
    iotop -oP > $fileName
    iostat -x -k -d 1 2 >> $fileName
    top >> $fileName

    crontab -e 

4. #/bin/bash
   export FILE_NAME=performance-monitor-`data "+%Y-%m-%d %H:%M:%S"`.log
   touch $FILE_NAME
   echo "top monitor" > $FILE_NAME
   top -b -n 2 >> $FILE_NAME
   echo "iostat monitor" > $FILE_NAME
   iostat -d -x2 >> $FILE_NAME
   echo "iotop monitor" >> $FILE_NAME
   iotop -b -n 2 >> $FILE_NAME
   echo "mysql status monitor" >> $FILE_NAME
   mysqladmin -uroot -proot proc stat
   echo "mysql status monitor" >> $FILE_NAME
   mysql -uroot -proot -e 'SELECT trx_state,trx_query FROM information_schema.INNODB_TRX;' >> $FILE_NAME

