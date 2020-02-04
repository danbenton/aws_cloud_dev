# AWS KMS 101    
AWS Key Management Service is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.  
AWS KMS is integrated with other AWS services including EBS, Se, Amazon Redshift, Amazon Elastic Transcoder, Amazon WorkMail, Amazon Relational Database Service (RDS), and others to make it simple to encrypt your data with encryption keys that you manage.   
 - Encryption keys are regional - encryption and decryption have to occur in the same region.   
## Exam Tips    
The Customer Master Key (CMK):     
  - alias 
  - creation data    
  - description     
  - key state (enabled vs. disabled)   
  - key material (either customer provided or AWS provided)   
  - **Can NEVER be exported**   
Setup a Customer Master Key:    
  - Create alias and description   
  - Choose material option...(Default let amazon)    
  - Define Key **Administrative Permissions**   
    - IAM users/roles that can administer (but not use) the key through the KMS API 
  - Define Key **Usage Permissions**  
    - IAM users/roles that can use the key to encrypt and decrypt data     
 **Key Material Options**   
 - Use KMS generated key material   
 - Use your own key material     
# KMS API Calls   
## KMS API Calls Exam Tips   
- `aws kms encrypt`   
- `aws kms decrypt` 
- `aws kms re-encrypt`   
  - The re-encrypt API call encrypts data on the server side with a new customer master key (CMK) without exposing the plaintext of the data on the client side. 
- `aws kms enable-key-rotation`   
# KMS Envelope Encryption    
## Exam Tips   
**The Customer Master Key**   
- CMK is used to decrypt the data key (envelope key)   
- Envelope Key is used to decrypt the data   
Your Data key (also known as the Envelope key) is encrypted using the master key. This approach is known as Envelope encryption. 
# Other Notes: 
KMS is multi-tenant whereas CloudHSM is dedicated hardware. 
S3 Encryption and Client-Side encryption are not Key Management Solutions    

The Customer Master Key is used to encrypt and decrypt the Data Key or Envelope Key. 
The Data Key or Envelope Key is used to encrypt and decrypt your files. 
AWS Managed Customer Master Keys cannot be used to directly encrypt and decrypt files, since permissions cannot be changed to them.
Customer Managed Customer Master Keys can be used with the KMS command to encrypt the file, when Key Usage rights are given.
