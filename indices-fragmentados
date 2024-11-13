-- Seleciona índices fragmentados
SELECT 
    DB_NAME() AS DatabaseName,
    OBJECT_NAME(ips.object_id) AS TableName,
    i.name AS IndexName,
    ips.avg_fragmentation_in_percent AS FragmentationPercentage,
    ips.page_count AS PageCount
FROM 
    sys.dm_db_index_physical_stats(DB_ID(), NULL, NULL, NULL, 'SAMPLED') AS ips
JOIN 
    sys.indexes AS i ON ips.object_id = i.object_id AND ips.index_id = i.index_id
WHERE 
    ips.avg_fragmentation_in_percent > 10  -- Define um limite de fragmentação
    AND ips.page_count > 1000              -- Evita pequenos índices com pouca relevância
ORDER BY 
    FragmentationPercentage DESC;
