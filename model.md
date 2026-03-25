# 数据库表结构设计

## 1. 学生表 (students)
```sql
CREATE TABLE students (
    student_id VARCHAR(20) PRIMARY KEY COMMENT '学号',
    name VARCHAR(50) NOT NULL COMMENT '姓名',
    gender ENUM('男', '女') NOT NULL COMMENT '性别',
    birth_date DATE COMMENT '出生日期',
    major VARCHAR(100) COMMENT '专业',
    enrollment_year YEAR COMMENT '入学年份',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
