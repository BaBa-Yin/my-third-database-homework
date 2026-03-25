
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

CREATE TABLE courses (
    course_id VARCHAR(20) PRIMARY KEY COMMENT '课程号',
    course_name VARCHAR(100) NOT NULL COMMENT '课程名称',
    teacher_id VARCHAR(20) COMMENT '授课教师',
    credit DECIMAL(3,1) NOT NULL COMMENT '学分',
    semester VARCHAR(20) COMMENT '开课学期，如2024-1',
    description TEXT COMMENT '课程描述',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    FOREIGN KEY (teacher_id) REFERENCES teachers(teacher_id)
) COMMENT='课程信息表';

CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY COMMENT '选课记录ID',
    student_id VARCHAR(20) NOT NULL COMMENT '学号',
    course_id VARCHAR(20) NOT NULL COMMENT '课程号',
    score DECIMAL(5,2) COMMENT '成绩（0-100）',
    grade VARCHAR(10) COMMENT '等级（A/B/C/D/F）',
    exam_date DATE COMMENT '考试日期',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP COMMENT '选课时间',
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id),
    UNIQUE KEY uk_student_course (student_id, course_id) COMMENT '防止重复选课'
) COMMENT='选课成绩表';
###
##