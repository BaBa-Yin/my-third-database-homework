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

## 2.教师表 
CREATE TABLE teachers (
    teacher_id VARCHAR(20) PRIMARY KEY COMMENT '教师工号',
    name VARCHAR(50) NOT NULL COMMENT '姓名',
    gender ENUM('男', '女') NOT NULL COMMENT '性别',
    department VARCHAR(100) COMMENT '所属院系',
    title VARCHAR(50) COMMENT '职称（教授/副教授/讲师等）',
    email VARCHAR(100) COMMENT '邮箱',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间'
) COMMENT='教师信息表';