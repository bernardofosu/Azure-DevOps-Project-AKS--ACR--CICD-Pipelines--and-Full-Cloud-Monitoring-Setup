# 📘 Notes: Creating an Azure Subscription

## 1️⃣ Go to Subscriptions
- Open **Azure Portal**
- Search **Subscriptions**
- Click **➕ Add**

---

## 2️⃣ Basics Tab
Fill in the following:

- **Subscription name** → e.g., *Dev Subscription*
- **Billing account** → Auto-filled
- **Billing profile** → Select your billing profile
- **Invoice section** → Select your invoice
- **Plan** → *Microsoft Azure Plan*

💡 *This section controls billing and links the subscription to your tenant.*

---

## 3️⃣ Advanced Tab
- **Subscription directory** → Your Azure AD Tenant
- **Management group** → *Root Management Group*
- **Subscription owner** → Your email

⚙️ *Used for governance and directory placement.*

---

## 4️⃣ Budget Tab (Optional but Recommended)
Set cost limits:

- **Budget Name** → e.g., *Dev-Budget*
- **Amount** → Enter USD amount
- **Alert condition** → e.g., 100% alert

📩 Alerts are emailed to the subscription owner.

---

## 5️⃣ Tags Tab (Optional)
Useful for cost reporting & automation.

Example Tags:
- **Environment:** Dev
- **Owner:** Bernard
- **Project:** TestLab

🏷 Tags help with resource organization and governance.

---

## 6️⃣ Review + Create
- Review all settings
- Click **Create**

🎉 The subscription is now provisioned.

---

## 📚 Summary
1. Subscriptions → **+ Add**  
2. Fill **Basics**  
3. Set **Advanced**  
4. Add **Budget** (optional)  
5. Add **Tags** (optional)  
6. **Review + Create**

---

Made with ❤️ for your Azure learning journey.
