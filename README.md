# Alfresco Backup 
Alfresco backup script - Based on backup script written by Chris Newald avaliable in https://community.alfresco.com/thread/202783-backup-and-restore-procedures

To restore backups made by this script use script avaliable in https://github.com/bruno-oliveira1/alfresco-restore

Tested only in Linux environment

To install haveged 
https://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged

To generate gpg key
https://www.digitalocean.com/community/tutorials/how-to-use-duplicity-with-gpg-to-securely-automate-backups-on-ubuntu

Download latest version of duplicity in http://savannah.c3sl.ufpr.br/duplicity/
Eg: wget http://savannah.c3sl.ufpr.br/duplicity/duplicity-0.7.15.tar.gz
tar xvf duplicity-0.7.15.tar.gz
See README file into duplicity-0.7.15 folder to get instructions how to install duplicity and your dependences  

Change variables in the script 
Use \ before / in path values
Eg: Change /backup/alfresco to /root 
sed -e 's/\/backup\/alfresco/\/root/g -i /path_to_alfrescobackup_script/alfrescobackup

Change various values in a single line
sed -e 's/259/10/g;s/KEYVALUE/AAAAAAAAAA/g;s/\/backup\/alfresco/\/root/g;s/POSTPASS/password/g;s/GPGPASS/gpgpssword/g;s/11M/1M/g;s/66W/6W/g;s/111/1/g;' /path_to_alfrescobackup_script/alfrescobackup -i /path_to_alfrescobackup_script/alfrescobackup

Before change 

DUMP_NUM=259				         	                           # Number of DB backups to keep,

GPG_KEY='KEYVALUE'                                       # Use gpg --list-keys to get your keys

TARGET='file:///backup/alfresco'                         # The path to where we want to store the backup

TARGET2='/backup/alfresco'                               # The path to where we want to store the postgres backup

POSTGRESPASS="POSTPASS"                                  # Postgresql password

PHRASE="GPGPASS"                                         # GPG password

BK_FULL_FREQ="11M" 			                          		   # Create a new full backup every 1 month

BK_FULL_LIFE="66W" 					                             # Delete any backup older than 6 weeks

BK_KEEP_FULL="111" 					                             # How many full+inc cycle to keep

After change 

DUMP_NUM=10				         	                             # Number of DB backups to keep,

GPG_KEY='AAAAAAAAAA'                                     # Use gpg --list-keys to get your keys

TARGET='file:///root'                                    # The path to where we want to store the backup

TARGET2='/root'                                          # The path to where we want to store the postgres backup

POSTGRESPASS="psssword"                                  # Postgresql password

PHRASE="gpgpassword"                                     # GPG password

BK_FULL_FREQ="1M" 			                          		   # Create a new full backup every 1 month

BK_FULL_LIFE="6W" 					                             # Delete any backup older than 6 weeks

BK_KEEP_FULL="1"  					                             # How many full+inc cycle to keep
