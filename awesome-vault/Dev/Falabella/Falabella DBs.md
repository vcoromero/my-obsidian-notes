**Test** 

- **MYSQL_HOST:** cmr-mx-onboarding-test.mysql.database.azure.com 
- **MYSQL_SERVICEUSER_USER:** cTgNpZvT@cmr-mx-onboarding-test 
- **MYSQL_SERVICEUSER_PASSWORD:** S-d3>VG0q6C<5EqqSpa67mGFbYs_fU61 

**QA** 

- **MYSQL_HOST:** cmr-mx-onboarding-qa.mysql.database.azure.com 
- **MYSQL_SERVICEUSER_USER:** enZupQuR@cmr-mx-onboarding-qa 
- **MYSQL_SERVICEUSER_PASSWORD:** AIhvz5GGIH6IQNAIi<LjZj7Qncb=e<og 

**Producción:** 

- **MYSQL_HOST**=cmr-mx-onboarding-prod.mysql.database.azure.com 
- **MYSQL_USER**=GdscsZufwYxqEuQk@cmr-mx-onboarding-prod 
- **MYSQL_PASSWORD**=HA0T34QvdfvA38HlvXQj*lw4pFTkpgZ7


Queries:

select * from run_tasks where rtas_person_id = 'ropv950219htcmrc53' order by rtas_created desc LIMIT 30;
select dt.dtas_id, rt.rtas_created, rt.rtas_session_id, dt.dtas_code, rt.rtas_status, ct.cota_content from run_tasks rt  
inner join def_tasks dt on dt.dtas_id = rt.dtas_id 
inner join content_tasks ct on ct.cota_id = rt.rtas_id 
where rt.rtas_flow_id = '9e97ff610c1547b847ec55858a13cd250dd267f59928'