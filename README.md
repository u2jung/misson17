# misson17

# 1. ERD 다이어그램의 캡쳐본
<img width="914" alt="스크린샷 2025-03-14 09 49 02" src="https://github.com/user-attachments/assets/97391bd7-25d9-4ff0-a6a6-0a4550090a29" />

---

# 2.  DDL 문
CREATE SCHEMA `FandomK` DEFAULT CHARACTER SET utf8mb4 ;
USE FandomK;

CREATE TABLE w_idol (
	w_idol_name VARCHAR(255) NOT NULL PRIMARY KEY,
	group_name VARCHAR(255) NOT NULL
);

CREATE TABLE m_idol (
	m_idol_name VARCHAR(255) NOT NULL PRIMARY KEY,
	group_name VARCHAR(255) NOT NULL
);

CREATE TABLE my_page (
	user_name VARCHAR(225) NOT NULL PRIMARY KEY,
    credits INT,
    interest VARCHAR(225),
    w_idol_name VARCHAR(225),
    m_idol_name VARCHAR(225),
    FOREIGN KEY (w_idol_name) REFERENCES w_idol(w_idol_name),
    FOREIGN KEY (m_idol_name) REFERENCES m_idol(m_idol_name)
);

CREATE TABLE sponsor (
	spon_id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
	sponsor_type VARCHAR(255) NOT NULL,
	cost INT NOT NULL,
    donation INT,
    w_idol_name VARCHAR(255),
	m_idol_name VARCHAR(255),
    user_name VARCHAR(255) NOT NULL,
    FOREIGN KEY (w_idol_name) REFERENCES w_idol(w_idol_name),
    FOREIGN KEY (m_idol_name) REFERENCES m_idol(m_idol_name),
    FOREIGN KEY (user_name) REFERENCES my_page(user_name),
    CHECK(
		(w_idol_name IS NOT NULL AND m_idol_name IS NULL)
        OR (w_idol_name IS NULL AND m_idol_name IS NOT NULL)
    )
);

CREATE TABLE vote(
	vote_id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    total_votes INT NOT NULL,
    w_idol_name VARCHAR(255),
	m_idol_name VARCHAR(255),
    user_name VARCHAR(255) NOT NULL,
    FOREIGN KEY (w_idol_name) REFERENCES w_idol(w_idol_name),
    FOREIGN KEY (m_idol_name) REFERENCES m_idol(m_idol_name),
    FOREIGN KEY (user_name) REFERENCES my_page(user_name),
    CHECK(
		(w_idol_name IS NOT NULL AND m_idol_name IS NULL)
        OR (w_idol_name IS NULL AND m_idol_name IS NOT NULL)
    )
);

---
# 3. DB Tool에서 확인한 ERD 다이어그램
![misson17_ERD](https://github.com/user-attachments/assets/170d44d2-b5a8-4a08-b5dd-20fa41368aa5)
