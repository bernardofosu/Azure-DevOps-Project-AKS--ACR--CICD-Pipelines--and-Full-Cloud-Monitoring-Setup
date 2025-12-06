# 🎉 Azure Artifacts Maven Feed Setup Guide

Your step‑by‑step markdown guide with emojis, ready for Canva formatting.

---

# 📦 Azure Artifacts + Maven Integration

Azure Artifacts allows you to host Maven packages securely inside Azure DevOps. To publish Maven artifacts (JAR/WAR files) to your feed, update your `pom.xml` and `settings.xml` accordingly.

---

# 🏗️ Project Requirements

- ✔️ Java project using Maven
- ✔️ Azure DevOps project + Feed created
- ✔️ Personal Access Token (PAT) with **Packaging (Read & Write)** permissions
- ✔️ Update `pom.xml` and local `settings.xml`

---

# 🧭 1. Add Azure Artifact Feed to pom.xml

Locate your `<distributionManagement>` section and replace it with your Azure feed.

### 🔄 Replace old Nexus/Artifactory URLs like:

```xml
<distributionManagement>
  <repository>
    <id>maven-releases</id>
    <url>http://54.159.51.117:8081/repository/maven-releases</url>
  </repository>
  <snapshotRepository>
    <id>maven-snapshots</id>
    <url>http://54.159.51.117:8081/repository/maven-snapshots</url>
  </snapshotRepository>
</distributionManagement>
```

### ✅ Replace with Azure Artifacts:

```xml
<distributionManagement>
  <repository>
    <id>AzureDevOps-Feed</id>
    <url>https://pkgs.dev.azure.com/YOUR_ORG/YOUR_PROJECT/_packaging/YOUR_FEED/maven/v1</url>
  </repository>

  <snapshotRepository>
    <id>AzureDevOps-Feed</id>
    <url>https://pkgs.dev.azure.com/YOUR_ORG/YOUR_PROJECT/_packaging/YOUR_FEED/maven/v1</url>
  </snapshotRepository>
</distributionManagement>
```

💡 Azure uses **one endpoint** for both releases and snapshots.

---

# 🗂️ 2. Add Feed to Repositories Section

Add this inside the `<repositories>` block:

```xml
<repository>
  <id>AzureDevOps-Feed</id>
  <url>https://pkgs.dev.azure.com/YOUR_ORG/YOUR_PROJECT/_packaging/YOUR_FEED/maven/v1</url>
  <releases><enabled>true</enabled></releases>
  <snapshots><enabled>true</enabled></snapshots>
</repository>
```

This allows Maven to **download dependencies** from the feed.

---

# 🔐 3. Configure Authentication (settings.xml)

Edit this file:

```
~/.m2/settings.xml
```

Add:

```xml
<settings>
  <servers>
    <server>
      <id>AzureDevOps-Feed</id>
      <username>AzureDevOps</username>
      <password>YOUR_PERSONAL_ACCESS_TOKEN</password>
    </server>
  </servers>
</settings>
```

⚠️ Your PAT should NOT be uploaded to GitHub or Azure Repos.

---

# ▶️ 4. Publishing Artifacts

Run:

```bash
mvn deploy
```

Your JAR/WAR will now appear in:
**Azure DevOps → Artifacts → Your Feed** 🎉

---

# 🔍 5. Troubleshooting

| Issue            | Cause                           | Fix                                                  |
| ---------------- | ------------------------------- | ---------------------------------------------------- |
| 401 Unauthorized | Wrong PAT or server ID mismatch | Ensure `<id>` matches pom.xml                        |
| Feed not found   | Wrong URL                       | Copy from Azure DevOps → Artifacts → Connect to Feed |
| Deploy fails     | Missing distributionManagement  | Add section above                                    |

---

# 🎯 Summary

- 🔗 Add Azure feed to pom.xml
- 🔐 Configure PAT in settings.xml
- ☁️ Publish with `mvn deploy`
- 🎉 Packages appear in Azure Artifacts

If you want, I can also generate:
✨ Azure Pipeline YAML for automatic publishing
✨ Full Java project template
✨ A Canva-exportable PDF version of this file

Just ask! 😊
