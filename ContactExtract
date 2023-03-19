mport imaplib, email, getpass
from email.utils import getaddresses

#personal data has been removed for safety
imap_server =''
imap_user = ''
imap_password = ''

conn = imaplib.IMAP4_SSL(imap_server)
(retcode, capabilities) = conn.login(imap_user, imap_password)

conn.list()

conn.select("Inbox", readonly=True)
result, data = conn.uid('search', None, 'ALL')
uids = data[0].split()

result, data = conn.uid('fetch',  b','.join(uids),'(BODY[HEADER.FIELDS (FROM)])')
raw_file = open('raw-email-rec.tsv', 'w')

for i in range(0, len(data)):
     
    if len(data[i]) != 2:
        continue
     
    
    #The formatting library was not functioning, so I opted for manual formatting
    #Will try to fix in future
    #msg = email.message_from_string(str(data[i][1]))
    #senders = msg.get_all('from', [])
     
    row = str(data[i][1])
     
    row += "\n"
     
    
    raw_file.write(row)
raw_file.close()
conn.logout()
