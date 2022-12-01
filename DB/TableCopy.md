# 테이블 복사하고자 할 때

### 구조만 들고 올 때
CREATE TABLE IF NOT EXISTS `복사 테이블` LIKE `원본 테이블`;

### 구조와 데이터를 같이 들고 올 때
CREATE TABLE `복사 테이블` SELECT * FROM `원본 테이블`;

### 테이블 구조만 있고 데이터를 넣고 싶을 때
INSERT INTO `복사 테이블` SELECT * FROM `원본 테이블`;