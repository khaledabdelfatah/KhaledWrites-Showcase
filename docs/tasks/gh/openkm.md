
# **OpenKM Guide**

## **What is OpenKM?**

OpenKM is a document management system that allows you to manage, share, and collaborate on documents and information within your organization. It provides a centralized repository for storing documents, version control, access control, and workflow management.

## **How to Install OpenKM**

### **Prerequisites**

Before installing OpenKM, ensure you have the following prerequisites:

1. Java 8 (OpenJDK 8 recommended) installed on your system.
2. Working OpenOffice or LibreOffice installation for document preview.
3. MySQL or PostgreSQL database server installed and running.

### **Installation Steps**

There are two main methods for installing OpenKM

1. Using the Installer
2. Manual Installation

#### **Using the Installer**

1. Download the installer (OKMInstaller.jar) from SourceForge or the OpenKM website.
2. Move the installer to the desired installation directory and run it using the following command: `java -jar OKMInstaller.jar`
3. Follow the text-based installation prompts to configure the setup. Dependencies like ImageMagick and LibreOffice will be installed automatically if required.
4. Once the installation is complete, start the OpenKM service using the following command: `service openkm start`

#### **Manual Installation**

1. Download the OpenKM bundle (e.g., OpenKM-6.x.x-community-tomcat-bundle.zip).
2. Uncompress the file in your desired directory (e.g., /opt/ on Linux or C:\ on Windows).
3. Start Tomcat and configure OpenKM according to its documentation.

## **How to Create Categories**

Categories in OpenKM are used to organize and classify documents based on their content or purpose. Here's how you can create categories in OpenKM:

1. Log in to the OpenKM web interface using your credentials and navigate to the properties panel of a document.
2. Select the "Category" option and assign a category (e.g., Management, Project, Region).
3. Sub-categories can also be created for further organization, allowing documents to appear under multiple categories without duplication.

## **How to Manage Categories Access Writes**

In OpenKM, access rights for categories can be managed to control who can view, edit, or delete documents within specific categories. Here's how you can manage access rights for categories:

1. Use OpenKM's administration interface to define user roles and permissions.
2. Assign specific permissions (read, write, delete) for categories based on user roles.
3. Ensure proper configuration of roles within the system to restrict or allow access to categorized content.

---
References:

- [OpenKM Documentation](https://www.openkm.com/wiki/index.php/Installation_Guide)
- [Adding Categories in OpenKM](https://www.openkm.com/wiki/index.php/Adding_categories)
- [User Guide](https://www.openkm.com/wiki/index.php/User_Guide)
 