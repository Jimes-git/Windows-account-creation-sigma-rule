Description:
This is a test sigma rule yaml file that is able to detect if there is any local account creation in your windows system (EventID: 4720), it was tested against chainsaw using the following command
to see if it was able to find account creation when I created a test account named 'SigmaTestUser' using the windows event logs and chainsaw mapping files. This is a controlled experiment
so it does not establish false positive rates across other environments. It's important to note that legitimate account creation will still flag as a false positive

Logging requirements:
- Enable auditing for windows
- export the windows security event log after creating the test user
- Install chainsaw version 2.17.1 and mappings (sigma-event-logs-all) https://github.com/WithSecureOpenSource/chainsaw
- run the following command

Command for testing against chainsaw (given chainsaw and mappings are installed)
& "D:\chainsaw_x86_64-pc-windows-msvc\chainsaw\chainsaw.exe" hunt "D:\Chainsaw\Logs\Security.evtx" `
  -s "D:\Chainsaw\SigmaRules\win_security_user_account_created.yml" `
  --mapping "D:\chainsaw_x86_64-pc-windows-msvc\chainsaw\mappings\sigma-event-logs-all.yml" `
  --full
  
  Fields for investigation: Computer, SubjectUserName, SubjectDomainName, SubjectUserSid, SubjectLogonID, TargetUsername, TargetDomainName, TargetSid

  
