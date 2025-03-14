---
title: Changes in Access (Access desktop database reference)
TOCTitle: Changes in Access
description: Access does not include support for Access Data Projects (ADPs). Access introduces a new application type that enables you to create a web-based Access app.
ms:assetid: 8dfc5fc9-a6a7-4a91-8e97-c3874e9b880f
ms:mtpsurl: https://msdn.microsoft.com/library/JJ618413(v=office.15)
ms:contentKeyID: 49106417
ms.date: 10/16/2018
mtps_version: v=office.15
ms.localizationpriority: high
---

# Changes in Access

**Applies to:** Access 2013 | Office 2013

Access does not include support for Access Data Projects (ADPs). Access introduces a new application type that enables you to create a web-based Access app. By using this application type, you can create web-based applications that use the power of SQL Server on-premises or in the cloud.

In an Access app on SharePoint Server, when you create a table, a query, or a data macro in the Access client in which you are creating tables, views, or triggers in a SQL Server database, by using the Access client, you can open your database to other applications that connect to SQL Server. This enables you to share your data or load data from other systems into your Access app.

With Office 365 and Access, you can build applications that reach your users without having to worry about deployment challenges, software installation issues, or operating system compatibilities. Build your app in one location and share it across the web with the power of SQL Azure and SQL Server.

[SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), the cloud version of SQL Server, does not support features that Access Data Projects (ADPs) rely on to operate. To support ADPs on SQL Azure, Access would require significant changes.

For these reasons, Access does not support ADPs. ADPs have been a great tool for working with SQL Server in an on-premises environment; however, much has changed since ADPs were introduced in Access 2000. Users now expect their database to be available wherever they are.

## ADP support and the future

ADPs continue to work in earlier versions of Access. You can continue to develop your ADP applications and we will continue to support earlier versions of Access under the standard [support lifecycle](https://support.microsoft.com/lifecycle/search). We will not update older versions of Access to support new versions of SQL Server or SQL Azure. Therefore, you may encounter issues if you use SQL Server 2012 or later versions with your ADP. ADPs will continue to support SQL 2008 R2 and earlier.

For the future, ADP developers can consider several different possibilities:

- **Convert to an Access app** – Using Access, you can import your tables into a new Access app, and forms for your application are automatically created for you. You can extend the functionality of the base forms that Access creates for you, and users can use your application on the web. Although some of the functionality that you use in ADPs may not be available now, expect Microsoft to continue to focus improvements in the product for this application type.

- **Convert to a linked desktop database** – Access continues to support creating desktop databases in the .accdb file format. You can convert your application to the .accdb format, including all of your existing forms and reports, and leave the data in SQL Server. You can link to the SQL Server database by using linked tables, and your application will continue to operate against the same data.

- **Create a hybrid application** – If your application is large and you don’t want to convert everything at the same time, you can import your data into an Access app and link to the SQL Server database from an .accdb. This allows you migrate gradually, adding forms and functionality over time to your Access app, while maintaining your client application as an .accdb with linked tables to the SQL Server database behind the Access app.

- **Upgrade to the .NET Framework** – Your application may be complex enough to consider moving to a professional development platform such as the .NET Framework. SQL Server is designed to make it easier for you to use your existing database infrastructure and extend the functionality of your application without having to significantly rewrite your code.

## Conclusion

Access is designed to connect databases with the cloud by building on SharePoint Server and SQL Server technologies and easily work with Office 365. Access is designed to help you quickly create and share data-driven business apps that help run your business.

## See also

- [New in Access 2013 for developers](https://docs.microsoft.com/office/vba/access/concepts/miscellaneous/new-in-access-for-developers)


