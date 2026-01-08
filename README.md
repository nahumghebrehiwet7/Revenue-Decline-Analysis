# Revenue-Decline-Analysis
Finding potential solutions to address the decline in revenue 

# This shows veg and non-veg orders
SELECT t2.food_newtype, SUM(t1.quantity) AS Item_Quantity
FROM orders_items t1
LEFT JOIN (
SELECT item_id,
CASE
WHEN food_type LIKE 'veg%' THEN 'veg'
ELSE 'non-veg'
END AS food_newtype
FROM food_items
) t2 ON t1.item_id = t2.item_id
GROUP BY t2.food_newtype;

# This shows restaurants with highest orders
select RT.restaurant_name, RT.restaurant_id, RT.cuisine, sum(quantity) as Quantity_Of_Items
from restaurants RT
left join food_items FT on RT.restaurant_id = FT.restaurant_id
left join orders_items OT on FT.item_id = OT.item_id
group by RT.restaurant_id
order by Quantity_Of_Items desc
limit 10; 

# Restaurants with no orders 
select RT.restaurant_name, RT.restaurant_id, RT.cuisine, sum(quantity) as Quantity_Of_Items
from restaurants RT
left join food_items FT on RT.restaurant_id = FT.restaurant_id
left join orders_items OT on FT.item_id = OT.item_id
group by RT.restaurant_id
having Quantity_Of_Items is NULL 
order by Quantity_Of_Items desc;
