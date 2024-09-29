CREATE OR REPLACE PROCEDURE manage_records(
    p_id IN NUMBER,
    p_name IN VARCHAR2,
    p_city IN VARCHAR2,
    p_action IN VARCHAR2  -- 'INSERT', 'UPDATE', or 'DELETE'
) AS
BEGIN
    IF p_action = 'INSERT' THEN
        -- Insert into table A
        INSERT INTO table_a (id, name, city) VALUES (p_id, p_name, p_city);
        
        -- Insert into table B
        INSERT INTO table_b (id, name, city) VALUES (p_id, p_name, p_city);

    ELSIF p_action = 'UPDATE' THEN
        -- Update table A
        UPDATE table_a 
        SET name = p_name, city = p_city 
        WHERE id = p_id;
        
        -- Update table B
        UPDATE table_b 
        SET name = p_name, city = p_city 
        WHERE id = p_id;

    ELSIF p_action = 'DELETE' THEN
        -- Delete from table A
        DELETE FROM table_a WHERE id = p_id;
        
        -- Delete from table B
        DELETE FROM table_b WHERE id = p_id;
    END IF;

    COMMIT;  -- Commit the transaction if needed
END;
/
BEGIN
    manage_records(1, 'Jane Doe', 'Los Aeles', 'UPDATE');
END;
====================
--trigger to update particular one field in taba where anthing insert on tabb
create or replace trigger updcav
after insert or update or delete on tabb
for each row
begin
if INSERTING OR UPDATING THEN
 update taba set caveat_no=:new.caveat_no where case_no=:new.case_no;
 ELSIF DELETING THEN
        UPDATE taba
        SET caveat_no = NULL
        WHERE case_no = :old.case_no;
    END IF;
end;
=================
create or replace trigger deletestu
before delete on stuinfo
for each row
begin
insert into detstuinfo values(:old.id,:old.name,:old.city);
end;
==================
