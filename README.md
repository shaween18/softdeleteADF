# softdeleteADF
 
I have provided the templates for the pipeline. It includes the datasets, linked services, and pipeline. 

The entire BackupContacts Pipeline can be found in the workplace_publish branch.

Steps for creation of watermark table:
 
1. Create a watermark table in SSMS:

		CREATE TABLE [dbo].[SqlTableWatermark](
		[TableName] [varchar](255) NULL,
		[WatermarkValue] [datetime] NULL
		)

2. Insert the TableName, along with an arbitrary date value for the WatermarkValue provided below:

		INSERT INTO SQLTableWatermark(TableName, WatermarkValue)
		VALUES ('contacts', '1970/01/01')
		
3. Create a stored procedure that updates the last modified date. For the purposes of this demo, I have kept it very simple, but please feel free to add anything else.

		CREATE PROCEDURE [dbo].[update_sqltablewatermark] @LastModifiedtime datetime, @TableName varchar(50)
		AS

		BEGIN

		 UPDATE SqlTableWatermark
		SET [WatermarkValue] = @LastModifiedtime
		WHERE [TableName] = @TableName

		END
		
Screenshots of the pipeline are provided in the Screenshots folder for each step of the pipeline (Lookup activity, Copy data Activity, and Stored procedure activity).

