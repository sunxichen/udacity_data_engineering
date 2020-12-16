# 简介

这个项目的背景是假设有一个音乐流媒体公司Sparkify, 他想分析他们在音乐流媒体应用上收集到的歌曲和用户活动数据。

本项目的目标是根据Star Schema进行表的设计，并创建 ETL pipeline来读取数据存入数据表。

# 项目描述

在这个项目中，我使用了Python以及Postgres进行数据建模，并构建ETL pipeline. 在关系型数据库data modeling方面，我采用了Star Schema定义了fact table与dimension table. 另一方面，用ETL pipeline将位于两个本地目录的文件中的数据传输到Postgres的表中。

# Star Schema

## Fact Table

- `songplays` : log data里的关于歌曲播放情况的数据，包含的列：`songplay_id` `start_time` (开始听歌时间)`user_id` `level` (用户的等级，free或paid，这里也可以放在users表里不在这里创建，但是可以根据query进行优化，把它从user表里拿出来) `song_id` `artist_id` `session_id` `location` (地理位置数据) `user_agent` (请求时的user_agent)

## Dimension Table

- `users`: 用户表，包含的列有，`user_id` `first_name` `last_name` `gender` `level`
- `songs`: 歌曲表，包含的列有，`song_id` `title` `artist_id` `year` `duration`
- `artists`: 艺人表，包含的列有，`artist_id` `name` `location` `lattitude` `longtitude`
- `time`: 时间表，根据数据里收集的歌曲播放点击播放的时间戳，分割成特定的单元，包含的列有，`start_time`(由时间戳转换的datetime类型) `hour` `day` `week` `month` `year` `weekday`

# 项目设计

数据库建模的设计即 Star Schema所述

ETL设计即用pandas读取json数据，然后进行parse，以合适的格式存入(比如timestamp转换为datetime)数据库

# 文件描述

`data.zip` 数据集

`create_tables.py` 创建数据库并创建表

`etl.py` 解析数据集并将数据load进数据库

`sql_queries.py` 一些用到的sql语句

# 项目流程

`create_tables.py` -> `etl.py`
