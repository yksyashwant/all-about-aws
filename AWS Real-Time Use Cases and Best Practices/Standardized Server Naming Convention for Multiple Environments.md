### Standardized Server Naming Convention for Multiple Environments

When naming servers for different environments (Dev, TEST, QA, UAT, Preprod,Prod, Infra ), it's important to use a consistent naming convention to make it clear which environment each server belongs to

### **General Naming Convention Format:**
`<env>-<os>-<app-name>-<region>-<instance_id>`

### **Breakdown:**

1. **Environment (env):**
   - `dev` (Development)
   - `test` (Testing)
   - `qa` (Quality Assurance)
   - `uat` (User Acceptance Testing)
   - `preprod` (Pre-production)
   - `prod` (Production)

2. **Operating System (os):**
   - `linux` or `win` (Windows)

3. **Application (app-name):**
   - The short name or acronym of the application or service, such as:
     - `payment`
     - `backend`
     - `frontend`
     - `database` (db)
     - `api`
     - `auth` (authentication service)

4. **Region (region):**
   - The region, data center, or geographical location, such as:
     - `us-east-1` (North Virginia)
     - `eu-west-1` (Ireland)
     - `asia-pacific-1` (Singapore)

5. **Instance ID (instance_id):**
   The EC2 instance ID is now included at the end, which would typically be the instance’s unique ID from AWS (e.g., i-0123456789abcdef0).
 

### **Linux Server Example (frontend application):**

1. **Development (dev) Environment:**
   - `dev-linux-frontend-us-east-1-i-0123456789abcdef0`

2. **Test (test) Environment:**
   - `test-linux-frontend-us-east-1-i-0abcdef1234567890`

3. **Quality Assurance (qa) Environment:**
   - `qa-linux-frontend-us-east-1-i-0abcd1234ef567890`

4. **User Acceptance Testing (uat) Environment:**
   - `uat-linux-frontend-us-east-1-i-01234abcd567890123`

5. **Pre-production (preprod) Environment:**
   - `preprod-linux-frontend-us-east-1-i-0123456789abcdef0`

6. **Production (prod) Environment:**
   - `prod-linux-frontend-us-east-1-i-0abcdef1234567890`

-

### **Windows Server Example (frontend application):**

1. **Development (dev) Environment:**
   - `dev-win-frontend-us-east-1-i-0123456789abcdef0`

2. **Test (test) Environment:**
   - `test-win-frontend-us-east-1-i-0abcdef1234567890`

3. **Quality Assurance (qa) Environment:**
   - `qa-win-frontend-us-east-1-i-0abcd1234ef567890`

4. **User Acceptance Testing (uat) Environment:**
   - `uat-win-frontend-us-east-1-i-01234abcd567890123`

5. **Pre-production (preprod) Environment:**
   - `preprod-win-frontend-us-east-1-i-0123456789abcdef0`

6. **Production (prod) Environment:**
   - `prod-win-frontend-us-east-1-i-0abcdef1234567890`
