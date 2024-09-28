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
