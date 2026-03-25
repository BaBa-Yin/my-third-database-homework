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
