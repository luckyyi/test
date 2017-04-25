# Fulfillment API
## fulfillment
- UpsertAccount when isClaimed
  - 根据CrmAccountId找到已有Account, 没有就New Account。
  - Upsert Account/Vendor/Contact
- UpsertUser
  - CreateProfile 或 BuildExistingProfile的时候，对User数据进行处理。
  - 根据Username查找已有User,没有就New User
  - 根据和Profile的关联进行查找相关数据，完成后和Profile进行关联。
