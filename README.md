# SAP-Queries
Vehicle Running Expense Query

SELECT 
	T1."DocNum" AS "SAP REF", 
	T1."DocDate" AS "DATE",
	T1."DocDueDate" AS "SYS DATE", 
	T0."Dscription" AS "DETAILS", 
	T0."OcrCode2" AS "ASSET", 
	T0."AcctCode" AS "ACCOUNT CODE", 
	T2."AcctName" AS "ACCOUNT NAME", 
	T0."PriceBefDi" AS "AMOUNT PAID"
FROM PCH1 T0  INNER JOIN OPCH T1 ON T0."DocEntry" = T1."DocEntry" INNER JOIN OACT T2 ON T0."AcctCode" = T2."AcctCode"
WHERE T1."DocDate" between [%0] and [%1] and T0."AcctCode" between 601010201 and 601010204 and T1."CANCELED" = 'N'

UNION ALL

SELECT 
	T0."DocNum" AS "SAP REF",
 	T0."DocDate" AS "DATE",
	T0."DocDueDate" AS "SYS DATE", 
	T0."JrnlMemo" AS "DETAILS", 
	T1."OcrCode2" AS "ASSET", 
	T1."AcctCode" AS "ACCOUNT CODE",
              T1."AcctName" as "ACCOUNT NAME",
	T1."SumApplied" AS "AMOUNT PAID"
FROM OVPM T0  INNER JOIN VPM4 T1 ON T0."DocEntry" = T1."DocNum" INNER JOIN OUSR T2 ON T0."UserSign" = T2."USERID"
WHERE T0."DocDate"  between [%0] and [%1] and T1."AcctCode" between 601010201 and 601010204 and  T0."Canceled" = 'N'
