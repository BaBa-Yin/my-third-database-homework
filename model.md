# 数据库表结构设计

## 1. 学生表 (students)

```sql
CREATE TABLE students (
    student_id VARCHAR(20) PRIMARY KEY COMMENT '学号，如2024001',
    name VARCHAR(50) NOT NULL COMMENT '姓名',
    gender ENUM('男', '女') NOT NULL COMMENT '性别',
    birth_date DATE COMMENT '出生日期',
    major VARCHAR(100) COMMENT '专业',
    enrollment_year YEAR COMMENT '入学年份',  -- 优化：从VARCHAR改为YEAR
    email VARCHAR(100) COMMENT '学校邮箱',     -- 新增字段
    phone VARCHAR(20) COMMENT '联系电话',
    status ENUM('在读', '休学', '毕业') DEFAULT '在读' COMMENT '学籍状态',  -- 新增字段
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间'
) COMMENT='学生信息表';

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