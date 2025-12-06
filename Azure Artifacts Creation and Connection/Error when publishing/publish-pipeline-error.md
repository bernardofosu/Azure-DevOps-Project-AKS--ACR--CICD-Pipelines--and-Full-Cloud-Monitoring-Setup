# 📘 Azure DevOps Maven Deployment – Fix Summary

## 🔐 1️⃣ Authentication Fix — Create Maven settings.xml
❌ Before Fix:
- 401 Unauthorized
- Could not transfer metadata  
- Failed to deploy artifact

🎉 Solution:
Create ~/.m2/settings.xml using System.AccessToken.

## 🔢 2️⃣ Versioning Fix — Auto-Increment SNAPSHOT Version
❌ Before Fix:
- 409 Conflict – SNAPSHOT version already used

🎉 Solution:
Automatically set version:
0.0.$(Build.BuildId)-SNAPSHOT

## 🛂 3️⃣ Permissions Fix — Build Service Missing Access
❌ Before Fix:
- 401 Unauthorized when contacting feed

🎉 Solution:
Give Azure DevOps Build Service → Feed Publisher or Feed Owner permission.

## 🌟 Final Results
✔ Deployment successful  
✔ Versioning automated  
✔ Authentication fixed  
✔ Permissions corrected  
