# MS-SQL-SEVRER--EXCEPTION
Exception of SQL Server

USE [PPAS_WEB]
GO
/****** Object:  StoredProcedure [dbo].[USP_DB_TRACE_ERROR_LOG]    Script Date: 01-06-2023 12:39:51 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
ALTER PROCEDURE [dbo].[USP_DB_TRACE_ERROR_LOG]
AS
 
BEGIN
  SET NOCOUNT ON 
  SET XACT_ABORT ON
  
  DECLARE @ErrorNumber VARCHAR(MAX)  
  DECLARE @ErrorState VARCHAR(MAX)  
  DECLARE @ErrorSeverity VARCHAR(MAX)  
  DECLARE @ErrorLine VARCHAR(MAX)  
  DECLARE @ErrorProc VARCHAR(MAX)  
  DECLARE @ErrorMesg VARCHAR(MAX)  
  DECLARE @vUserName VARCHAR(MAX)  
  DECLARE @vHostName VARCHAR(MAX) 

  SELECT  @ErrorNumber = ERROR_NUMBER()  
       ,@ErrorState = ERROR_STATE()  
       ,@ErrorSeverity = ERROR_SEVERITY()  
       ,@ErrorLine = ERROR_LINE()  
       ,@ErrorProc = ERROR_PROCEDURE()  
       ,@ErrorMesg = ERROR_MESSAGE()  
       ,@vUserName = SUSER_SNAME()  
       ,@vHostName = Host_NAME()  
  
INSERT INTO DB_ERROR_LOG(vErrorNumber,vErrorState,vErrorSeverity,vErrorLine,
	vErrorProc,vErrorMsg,vUserName,vHostName,dErrorDate)  
VALUES(@ErrorNumber,@ErrorState,@ErrorSeverity,@ErrorLine,@ErrorProc,
	@ErrorMesg,@vUserName,@vHostName,GETDATE())  
END 
