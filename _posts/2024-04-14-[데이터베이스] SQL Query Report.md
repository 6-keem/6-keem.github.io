---
title : "[데이터베이스] SQL Query Report"
date : 2024-04-14 21:43:00 +0900
categories : [Database, 과제]
tags : [database] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

# <문제 1>

## **3. 아래의 문제를 SQL로 작성한다.**

### **가. 과목명에 ‘구조’가 들어 있는 과목번호와 과목명을 찾아라.**

```sql
select course_id, title
from course
where title like '%구조%';
```

![1-1](https://github.com/6-keem/BlogImageRepository/assets/113224939/17ade1f4-bf72-4994-a351-1d3271cc1c3a)

### **나. 2012년도 1학기에 강의가 없는 교수의 이름을 찾아라.**

```sql
select name
from professor
where position = '교수' and prof_id not in (select prof_id
                     from class
                     where year = 2012 and semester = 1);
```

![1-2](https://github.com/6-keem/BlogImageRepository/assets/113224939/396f49d9-b69f-4647-bc6c-44a6e7d0fa93)

### **다. 2012년도 1학기에 한 과목도 수강하지 않은 학생의 학번과 이름, 학과명을 찾아라.**

```sql
select s.stu_id, s.name, d.dept_name
from student s, department d
where s.dept_id = d.dept_id and s.stu_id not in (select stu_id
                                                from takes t, class c 
                                                where t.class_id = c.class_id and year = 2012 and semester = 1);
```

![1-3](https://github.com/6-keem/BlogImageRepository/assets/113224939/ddb06204-0611-4241-81a1-613fa1b32d68)

### **라. 학과별 학생 수를 찾아라. (학과명, 학생수)**

```sql
select d.dept_name, count(s.stu_id)
from student s, department d
where s.dept_id = d.dept_id
group by d.dept_name;
```

![1-4](https://github.com/6-keem/BlogImageRepository/assets/113224939/2ac359a1-95aa-4421-a762-840da5cfd883)

### **마. 학번별 수강과목 수를 찾아라. (학번, 수강과목수)**

```sql
select stu_id, count(class_id)
from takes
group by stu_id;
```

![1-5](https://github.com/6-keem/BlogImageRepository/assets/113224939/f7221e0a-84ff-4853-a488-1af810b5f0a5)

### **바. 가장 최근에 임용된 교수(여기서 교수는 직급이 아닌 전체 교수를 의미함) 의 이름과 재직연수(2024년도 기준)를 찾아라.**

```sql
select name, (2024-year_emp) 재직연수
from professor
where year_emp >= all (select year_emp
                       from professor);
```

![1-6](https://github.com/6-keem/BlogImageRepository/assets/113224939/488fe231-34d5-4922-b482-15ea662081b0)

### **사. 같은 학과, 같은 주소를 갖는 학생 이름의 쌍을 찾아라. (이때, 동일인이 쌍으로 나와서도 안되며, 한번 나온 쌍은 순서를 바꿔서 나와서도 안된다. 즉, (김광식, 김광식) 안되며, (김광식, 김정현)이 나왔다면 (김정현, 김광식)은 나와서는 안된다.)**

```sql
select s1.name, s2.name
from student s1, student s2
where s1.address = s2.address and s1.dept_id = s2.dept_id and s1.name < s2.name;
```

![1-7](https://github.com/6-keem/BlogImageRepository/assets/113224939/01efcd86-8178-4b97-a5ea-e3a3bf3529d6)



---



# <문제 2>

### 5. 아래는 은행에서 고객의 예금정보를 저장하기 위한 테이블 스키마이다. 이 테이블 들에 대해서 주어진 물음에 답할 수 있는 select문을 작성하라.

##### 1) 모든 고객의 계좌번호, 이름, 그리고 예금 잔액을 검색하라. 

```sql
select d.deposit_num, c.name, d.balance
from client c, deposit d
where c.ssn = d.ssn;
```

![2-1](https://github.com/6-keem/BlogImageRepository/assets/113224939/f8bd56d1-e801-417f-8a1b-8420fb9a8db0)

##### 2) 이름이 ‘박지성’인 고객의 전화번호와 주민등록번호를 검색하라. 

```sql
select phone, ssn
from client
where name = '박지성';
```

![2-2](https://github.com/6-keem/BlogImageRepository/assets/113224939/a92ccd76-3220-4277-b88d-d632be9e7678)

##### 3) 지점 이름이 ‘성남지점’인 지점을 통해 개설된 모든 예금의 잔액을 검색하라. 

```sql
select balance
from deposit
where branch_name = '성남지점';
```

![2-3](https://github.com/6-keem/BlogImageRepository/assets/113224939/9c608bef-eedf-473f-a6ff-f62cbaa11f32)

##### 4) 지점장 이름이 ‘고희경’인 지점의 이름과 주소를 검색하라. 

```sql
select branch_name, address
from branch
where branch_head = '고희경';
```

![2-4](https://github.com/6-keem/BlogImageRepository/assets/113224939/2da73ede-9530-41ca-850e-65337ebe8d6d)

##### 5) 지점 이름이 ‘광주지점’인 지점의 지점장 이름과 주소를 검색하라. 

```sql
select branch_head, address
from branch
where branch_name = '광주지점';
```

![2-5](https://github.com/6-keem/BlogImageRepository/assets/113224939/6418a273-1742-47fc-b3bf-57d693c46ead)

##### 6) 이름이 ‘김기식’인 고객이 소유한 예금의 계좌번호, 개설지점의 이름, 잔액을 검색하라. 

```sql
select deposit_num, branch_name, balance
from deposit
where ssn in (select ssn
             from client
             where name = '김기식');
```

![2-6](https://github.com/6-keem/BlogImageRepository/assets/113224939/5057520a-dd46-455a-9c4a-482c0d4b09f7)

##### 7) ‘성남지점’에서 계좌를 개설한 고객의 이름과 주소, 그리고 예금 잔액을 검색하라. 

```sql
select c.name, c.address, d.balance
from client c, deposit d
where c.ssn = d.ssn and d.branch_name = '성남지점';
```

![2-7](https://github.com/6-keem/BlogImageRepository/assets/113224939/a688cddc-3c31-4605-8bf9-a977ed0d7f0f)

##### 8) ‘성남지점’에서 계좌를 개설한 고객 중 김씨 성을 가진 고객의 이름과 예금 잔 액을 검색하라.

```sql
select c.name, d.balance
from client c, deposit d
where c.ssn = d.ssn and d.branch_name = '성남지점' and c.name like '김%';
```

![2-8](https://github.com/6-keem/BlogImageRepository/assets/113224939/75255ee5-56f3-4c4b-90c1-1fa5127247c7)

##### 9) 예금 잔액이 10만원 이상인 계좌를 소유한 고객의 이름을 검색하라. 

```sql
select name
from client
where ssn in (select ssn
             from deposit
             where balance >= 100000);
```

![2-9](https://github.com/6-keem/BlogImageRepository/assets/113224939/a8955da5-dc10-46a0-83b1-a2ea04efcde4)

##### 10) 예금 잔액이 10만원 이상인 계좌가 개설된 지점의 이름과 지점장 이름을 검색 하라. 

```sql
select branch_name, branch_head
from branch
where branch_name in (select branch_name
                     from deposit
                     where balance >= 100000);
```

![2-10](https://github.com/6-keem/BlogImageRepository/assets/113224939/a85a4034-9569-4118-aa9e-c439e9af86ed)

##### 11) 예금을 개설한 지점의 지점장과 이름이 같은 고객이 소유한 예금의 계좌번호, 잔액, 그리고 개설지점 이름을 검색하라.

```sql
select d.deposit_num, d.balance ,d.branch_name
from deposit d, client c, branch b
where d.ssn = c.ssn and d.branch_name = b.branch_name and b.branch_head = c.name;
```

![2-11](https://github.com/6-keem/BlogImageRepository/assets/113224939/99f4b1a6-3766-4eba-87e0-20bacd52c6f6)

##### 12) ‘서울지점’에서 계좌를 개설한 고객들 중에서 남자 고객의 이름과 예금 잔액을 검색하라. 

```sql
select c.name, d.balance
from client c, deposit d
where c.ssn = d.ssn and branch_name = '서울지점' and c.ssn like '%-1%' or c.ssn like '%-3%';
```

![2-12](https://github.com/6-keem/BlogImageRepository/assets/113224939/e7d00a5a-1923-49a9-a456-25ca344b634e)

##### 13) 주민등록번호상의 생일이 3월인 모든 고객의 이름과 소유한 예금의 계좌번호를 검색하라. 

```sql
select c.name, d.deposit_num
from client c, deposit d
where c.ssn = d.ssn and c.ssn like '__03%';
```

![2-13](https://github.com/6-keem/BlogImageRepository/assets/113224939/9cf24819-47cc-492a-a91d-e6716cd388a0)

##### 14) 자신의 주소와 같은 지점에 계좌를 소유하고 있는 고객의 이름과 예금 잔액을 검색하라. 

```sql
select c.name, d.balance
from client c, deposit d, branch b
where c.ssn = d.ssn and d.branch_name = b.branch_name and c.address = b.address;
```

![2-14](https://github.com/6-keem/BlogImageRepository/assets/113224939/da229676-0543-4f0d-8c2c-15a1f2369a31)

##### 15) ‘성남지점’과 거래하고 있는 고객의 숫자를 검색하라. 

```sql
select count(distinct c.ssn)
from client c, deposit d
where c.ssn = d.ssn and branch_name = '성남지점';
```

![2-15](https://github.com/6-keem/BlogImageRepository/assets/113224939/965f869d-c958-4d04-ba76-37f5dc49b94f)

##### 16) 각 지점별 잔액의 총합을 검색하라. 

```sql
select branch_name, sum(balance)
from deposit
group by branch_name;
```

![2-16](https://github.com/6-keem/BlogImageRepository/assets/113224939/dad82254-3035-4e41-9fd2-b860fe4e72cb)

##### 17) 고객 이름별 예금 잔액의 총합을 검색하라. 

```sql
select c.name, sum(d.balance)
from client c, deposit d
where c.ssn = d.ssn
group by c.name;
```

![2-17](https://github.com/6-keem/BlogImageRepository/assets/113224939/bc050061-1d61-4c90-83fd-8f61fea9e547)

##### 18) 잔액의 합이 100만원 이상인 지점 이름과 잔액의 합을 검색하라. 

```sql
select branch_name, sum(balance)
from deposit
group by branch_name
having sum(balance) >= 1000000;
```

![2-18](https://github.com/6-keem/BlogImageRepository/assets/113224939/ea3fae7d-d72d-4ff2-9339-b16cede86109)

##### 19) 지점별로 예금 잔액이 100만원 이상인 고객의 숫자를 검색하라. 

```sql
select d.branch_name, count(distinct c.ssn)
from client c, deposit d
where c.ssn = d.ssn and d.balance >= 1000000
group by d.branch_name;
```

![2-19](https://github.com/6-keem/BlogImageRepository/assets/113224939/719ddfca-da7f-487c-8832-01be99b1df0f)

##### 20) 예금 계좌를 소유하고 있지 않은 고객의 이름과 전화번호를 검색하라.

```sql
select name, phone
from client
where ssn not in (select ssn
                 from deposit);
```

![2-20](https://github.com/6-keem/BlogImageRepository/assets/113224939/ba5e804e-4ef6-433a-840b-1e83c403a70c)