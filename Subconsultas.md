# TCS13 - Subconsultas event
### Luis Tinoco 

1. **Primera Subconsulta: Esta consulta selecciona tres columnas de la tabla register: id y registered_at directamente, y speaker utilizando una subconsulta para obtener el nombre del orador desde la tabla conference basado en conference_id de cada registro en register**
2. 
   ```sql
    SELECT 
    r.id, 
    r.registered_at, 
    (SELECT c.speaker FROM conference c WHERE c.id = r.conference_id) AS speaker
    FROM 
    register r;


![alt text]( Imagenes/Opera%20Instantánea_2024-07-01_103223_api.elephantsql.com.png)

1. **Segunado Subconsulta: Esta consulta selecciona el id y code de cada registro en la tabla register, junto con el nombre completo (fullname) y el correo electrónico (email) del miembro asociado a través del member_id. Se filtra para incluir solo los registros cuyo member_id existe en la tabla member, asegurando datos válidos y completos en la consulta final.**
   ```sql
   SELECT 
    r.id, 
    r.code, 
    (
        SELECT m.fullname 
        FROM member m 
        WHERE m.id = r.member_id
    ) AS fullname, 
    (
        SELECT m.email 
        FROM member m 
        WHERE m.id = r.member_id
    ) AS email
    FROM 
    register r
    WHERE 
    r.member_id IN (SELECT id FROM member);



![alt text](Imagenes/Opera%20Instantánea_2024-07-01_111231_api.elephantsql.com.png)

