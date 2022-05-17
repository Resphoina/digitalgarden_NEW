---
{"dg-publish":true,"permalink":"/old/untitled-1-mps/","dgHomeLink":true,"dgPassFrontmatter":false}
---


(Home)[https://DigitalGarden.netlify.app/]


# <font color=#DC143C>()-()-()-()-(算法原子)</font>
URL:: 

```
dataview
table without id 萃取函数, 萃取解法
where contains(TITLES, "")
```














MPS核查重复门店号
```SQL
--↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹↹[MPS核查重复门店号]
--⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶[DECLARE]
DECLARE @STORECODE VARCHAR(200);
DECLARE @DATABASE INT;
--⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶[SET]
SET @STORECODE = '';
SET @DATABASE = '555';
--⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶[178]
IF @DATABASE = '178'
BEGIN
     WITH REPEAT_ID
     AS (SELECT GID, COUNT(0) AS REPEAT_NUM
         FROM DATABASE_178.MStore.dbo.STORE WITH(NOLOCK)
         GROUP BY GID
         HAVING COUNT(0) > 1),
     REPEAT_DETAIL
     AS (SELECT *
         FROM DATABASE_178.MStore.dbo.STORE WITH(NOLOCK)
         WHERE CompanyCode = 'GD'
         AND LEFT(CODE, 1) != 'C'
         AND EXISTS(SELECT * FROM REPEAT_ID WHERE REPEAT_ID.GID = STORE.GID))
     SELECT *
     FROM REPEAT_DETAIL WITH(NOLOCK)
     WHERE(CASE WHEN LEN(@STORECODE) > 0 THEN @STORECODE ELSE CODE END) = CODE
     ORDER BY GID
END
--⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶[587]
IF @DATABASE = '587'
BEGIN
     WITH REPEAT_ID
     AS (SELECT GID, COUNT(0) AS REPEAT_NUM
         FROM DATABASE_5_87.MStore.dbo.STORE WITH(NOLOCK)
         WHERE LEFT(CODE, 1) != 'C'
         GROUP BY GID
         HAVING COUNT(0) > 1),
     REPEAT_DETAIL
     AS (SELECT *
         FROM DATABASE_5_87.MStore.dbo.STORE WITH(NOLOCK)
         WHERE EXISTS(SELECT * FROM REPEAT_ID WHERE REPEAT_ID.GID = STORE.GID))
     SELECT *
     FROM REPEAT_DETAIL WITH(NOLOCK)
     WHERE(CASE WHEN LEN(@STORECODE) > 0 THEN @STORECODE ELSE CODE END) = CODE
     ORDER BY GID
END
--⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶⇶[555]
IF @DATABASE = '555'
BEGIN
     WITH REPEAT_ID
     AS (SELECT GID, COUNT(0) AS REPEAT_NUM
         FROM DATABASE_5_55.MStore.dbo.STORE WITH(NOLOCK)
         GROUP BY GID
         HAVING COUNT(0) > 1),
     REPEAT_DETAIL
     AS (SELECT *
         FROM DATABASE_5_55.MStore.dbo.STORE WITH(NOLOCK)
         WHERE EXISTS(SELECT * FROM REPEAT_ID WHERE REPEAT_ID.GID = STORE.GID))
     SELECT *
     FROM REPEAT_DETAIL WITH(NOLOCK)
     WHERE(CASE WHEN LEN(@STORECODE) > 0 THEN @STORECODE ELSE CODE END) = CODE
     ORDER BY GID
END
```