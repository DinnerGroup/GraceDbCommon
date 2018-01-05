# GraceDbCommon
Easy SQL or Maybe FTP tools

for unix/linux
Connect to oracle database, Thank you cx_Oracle
Make sure you have this path where the config/log file located
config path:/usr1/config
log path:/usr1/log/python

#cat DbConfig.ini
#the config file like:
#oracle tns
[oracle_server1]
host=xxx.xxx.xxx.xxx
port=1521
user=xxxxx
passwd=xxxxxx
sid=xxx

#hive
[hive_server1]
host=xxx.xxx.xxx.xxx
port=10000
user=xxxxx
passwd=xxxxx
database=default

if you connect to oracle, then the log locate will at /usr1/log/python/oracle
else if you connect to hive, then the log locate will at /usr1/log/python/hive
fi
Python Script Log in /usr1/log/python/oracle/your_python_script.log
#python script example:
#!/usr/bin/python2.7
# -*- coding:utf-8 -*-
import GraceDbCommon.oracle_common as orcl
conn = orcl.oracle_common(oracle_server1)
conn.connect()

#Every #DEBUG or #INGORE_ERROR or SQL sentence, don't forget end with ";"
v_sql = '''
#DEBUG: create a test table;
#INGORE_ERROR:drop table etl.test_table;
create table etl.test_table(a int);
#or some sql else
commit;
'''
conn.batch_execute_sql(v_sql)
exit()

#end

#####################################################################
New Class For SFTP by Paramiko, Thank you Paramiko
###config file:/usr1/config/sftp_config.ini
#cat /usr1/config/sftp_config.ini you'll see
#[server_xxx]
#host=xxx.xxx.xxx.xxx
#port=22
#user=root
#passwd=123456

python code like:
#!/usr/bin/python2.7
# -*- coding:utf-8 -*-
from GraceDbCommon import sftp_common
sftp=sftp_common("server_xxx")
sftp.sftp_conn()
sftp.sftp_put("/usr1/config/sftp_config.ini", "/data1/sftp_config.ini")
sftp.sftp_get("/data1/sftp_config.ini", "/usr1/sftp_config.ini")

#####################################################################
New Class For hive by pyhs2, Thank you pyhs2
#!/usr/bin/python2.7
# -*- coding:utf-8 -*-
from GraceDbCommon import hive_common
hive=hive_common("hive_server1")
hive.connect()
hive.batch_execute_sql("create table test_table(a int);")
######################################################################
