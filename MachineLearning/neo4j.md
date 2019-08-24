## Neo4j browser config

显示node数上限`:config initialNodeDisplay: 1000`

## Neo4j browser trick

* **将图片缩小**

  显示的图片是SVG格式的，在Chrome审查元素中将svg下的g作以下设置

```
<svg>
    <g transform="translate(0,0)scale(0.1)">...</g>
</svg>
```

## syntax

* load csv

```sql
load csv with headers from "file:///file.csv" as row
merge (a:Person {attr: row.from_node})
merge (b:Person {attr: row.to_node})
merge (a)-[:Edge {attr: row.edge}]->(b)
```

* show all

```sql
match p=(a)-[r]-(b)
return p
```

## demo

* cluster coefficient

```sql
match (u1:User)-[:InteractsWith]-(u2:User)
with u1, collect(distinct u2.id) as neighbors
match (a), (b)
where a.id in neighbors and b.id in neighbors
with u1, length(neighbors) * (length(neighbors) - 1) as total_num
    , sum(case when (a)-[:InteractsWith]->(b) then 1 else 0 end) as link_num
with u1, link_num * 1.0 / total_num as cluster_coef, link_num, total_num
order by cluster_coef desc
return u1.id, cluster_coef, link_num, total_num
```