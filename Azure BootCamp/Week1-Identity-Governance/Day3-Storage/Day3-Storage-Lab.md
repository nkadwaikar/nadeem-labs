# Day 3 — Azure Storage (Replication, Access, Private Endpoints)

## Chapters to Read
- Chapter 7 — Manage Azure Storage

## Learning Objectives
- Understand storage replication (LRS/ZRS/GRS)
- Configure secure access
- Deploy Private Endpoints
- Validate private connectivity

## Lab Steps
1. Create Storage Account
2. Configure replication (ZRS or GRS)
3. Disable public access
4. Create Private Endpoint
5. Link Private DNS Zone
6. Test access from VM
7. Validate DNS:
   ```bash
   nslookup <storageaccount>.blob.core.windows.net