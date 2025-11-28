+++
title = "About Me"
date = "2025-11-27"
author = "Xusheng Qian"
+++

## Hi, I'm Max

[LinkedIn](https://www.linkedin.com/in/xusheng-qian/) | [GitHub](https://github.com/qianxusheng) | [LeetCode](https://leetcode.com/u/max6666/)

I'm a graduate student pursuing a Master's degree in Information Science at the University of Pittsburgh, with a strong foundation in software engineering, machine learning, and full-stack development. My journey spans from electrical engineering to cutting-edge AI applications, driven by a passion for building impactful solutions.

---

## Education

**University of Pittsburgh** | Pittsburgh, PA
| *M.S. in Information Science* | Jan 2025 - Dec 2026
- Relevant Coursework: Machine Learning, Information System Design and Analysis (SDLC), Information Storage and Retrieval
- Skills: Java, JavaScript, TypeScript, Spring Boot, React.js, Angular
- Focus: My current journey centers on software engineering with a strong emphasis on web development. I'm actively expanding my expertise in distributed systems and exploring frontier technologies like Large Language Models (LLMs), while continuously strengthening my foundation in machine learning principles.

**Harbin University of Science and Technology** | Harbin, China
| *M.Eng. in Electrical & Computer Engineering* | Sep 2021 - Jun 2024
- Relevant Coursework: Optimization Methods & Convex Analysis, Advanced Linear Algebra & Matrix Theory, Stochastic Processes
- Skills: Signal Processing, Deep Learning, Fault Diagnosis, Machine Learning, MATLAB, Python, PyTorch, Tensorflow
- Focus: I was doing AI application research, specifically on fault diagnose track. It is like a research-based master degree.

**Shaoxing University** | Shaoxing, China
| *B.Eng. in Electrical Engineering* | Sep 2017 - Jun 2021
- Skills: C++, Python, MATLAB, Signal Processing
- Focus: In the first two years I was learning common fundamental courses like physics and calculus, and also some major specific courses like circuits (digital, analog), signals and systems, Microcontroller and also some programming class about C, assembly, Python, Matlab. In my last two years, I was more focusing on communication engineering track, taking courses like communication theory, coding theory, etc.
---

## Work Experience

### University of Pittsburgh School of Health and Rehabilitation Sciences
**Teaching Assistant** | Aug 2025 - Present
*HI 2453 Machine Learning*
- Teaching machine learning concepts using Google Colab, Python, and Jupyter Notebook

**Full Stack Engineer** | May 2025 - Present
- Developed a clinical research platform with Johns Hopkins University and UPMC for 200+ participants across multiple institutions, providing mobile app for participant symptom reporting and web portal for clinician workflows including session management, data review, and enrollment approval, utilizing agile development with weekly sprints
- Redesigned and implemented backend access control using REST APIs (Java/Spring Boot) and MySQL, creating admin table with one-to-one site mapping to separate super admin and local admin privileges, and refactoring related services to achieve multi-institutional data isolation for HIPAA compliance with scalable institution onboarding
- Optimized frontend applications using Angular/Ionic by upgrading the mobile app to Angular 17, enhancing UI and compatibility, and refining web portal features such as local admin registration, site management, and multi-level session dashboards, improving UX and code maintainability
- Built a content validation and evaluation platform with Next.js 15, Prisma, and PostgreSQL, enabling subject matter experts to validate structured content items with task management, progress tracking, and submission workflows, integrated with NextAuth authentication, Zod validation, Redis caching, and a modern shadcn/ui interface
- Integrated Redis to add session lifecycle control to stateless JWT authentication, caching token identifiers in blacklist and user registry for instant revocation and multi-session management capabilities

**Tech Stack:** Next.js, React.js, Spring Boot, Angular, Azure DevOps

### Genius Electronic Optical (Apple's lens supplier)
**Software Engineer** | Aug 2024 - Nov 2024 | Xiamen, China
- Developed industrial testing control software for camera lens manufacturing, integrating industrial camera SDK for automated image acquisition and implementing C++/OpenCV-based alignment calibration algorithms, reducing misalignment defect rate by 15%
- Implemented Python ETL pipeline integrating Kafka consumer API with PostgreSQL data warehouse for a new quality analytics use case, extracting and validating optical metrics using Pandas, reducing end-to-end processing time by 60%
- Engineered CNN-based lens flare detection application with Python/PyTorch and PyQt5 GUI to automate lens optical quality inspection, achieving 98% accuracy and reducing manual inspection workforce by 60%
- Collaborated with Apple camera team to port latest ISP calibration algorithms from MATLAB to C++, integrating into automated testing system, enabling seamless quality control for 100K+ daily iPhone lens output

**Tech Stack:** C++, Python, MATLAB, PyTorch

### Harbin University of Science and Technology
**Research Assistant** | Sep 2021 - Jun 2024 | Harbin, China
- Led cross-functional collaboration with manufacturing engineers to identify critical failure patterns in rotating machinery and operational pain points, developing and deploying AI-powered vibration analysis system that reduced unplanned downtime by 40% through early fault detection and prevention of severe failures across 3 facilities
- Built end-to-end ML data pipeline from hardware integration (motor drives, data acquisition, automated control) through data cleaning and validation, applying sliding window segmentation to generate and label 50K+ training samples from vibration signals
- Developed CNN and LSTM models using Python/TensorFlow for multi-class fault diagnosis across rotating machinery (rolling bearing, harmonic reducer), implementing signal processing pipeline with MATLAB for feature engineering and addressing class imbalance through weighted loss functions to achieve 98% accuracy

---

## Projects

### Information Retrieval System
*Aug 2025 - Nov 2025*
- Implemented document preprocessing pipeline in Java: tokenization, normalization, stopword filtering; TREC Text/Web format parsers; BufferedReader/Writer streaming for I/O optimization (700k documents)
- Built inverted index with block indexing and external k-way merge sort, leveraging optimized data structures: TreeMap to maintain ordered posting lists, PriorityQueue to optimize merge to O(n) complexity, StringBuilder to reduce indexing time by 75%
- Developed Query Likelihood model with Lucene: Dirichlet smoothing and Pseudo Relevance Feedback for query expansion; parameter optimization using NDCG metrics
- Built legal search system with Elasticsearch: Legal-BERT for dense semantic retrieval and Cross-encoder for two-stage reranking; Flask API and React frontend with Redis caching serving 200k legal cases

**Tech Stack:** Elasticsearch, Lucene, React.js, Flask

### NFL Player Performance Analysis: Bayesian Statistical Modeling with R
*Sep 2025 - Oct 2025*
- Performed Bayesian analysis on 1,000+ NFL players' catch rates using Beta-Binomial models and Empirical Bayes methods
- Evaluated multiple modeling approaches via Bayes Factor and cross-validation
- Developed R visualizations to identify undervalued talent and quantify performance risks for scouting decisions

**Tech Stack:** R, Machine Learning

### Kiddit: LLM-Powered Content Moderation Forum
*Jan 2025 - May 2025*
- Designed and implemented a Reddit-style social forum for children with JWT authentication, multi-level commenting, voting system, and community subscriptions. Containerized with Docker and configured CI/CD pipeline with GitHub Actions
- Integrated OpenAI API with Spring WebClient for real-time content moderation, detecting offensive language and hate speech, providing constructive feedback to users when comments are flagged inappropriate
- Designed 25+ RESTful APIs and 3NF-normalized MySQL schemas with 10+ tables, foreign key constraints, and composite indexes for forum features; implemented transactional services using JPA/Hibernate to ensure ACID compliance
- Delivered 20+ React components with TypeScript and TailwindCSS, supporting responsive design, theming and dark mode, improving feature delivery speed by 50% and ensuring UI consistency across 10+ devices

**Tech Stack:** React.js, Spring Boot, MySQL, OpenAI API, TypeScript, Tailwind CSS

### Pedometer Design and Implementation Based on STM32
*Nov 2020 - Apr 2021*
- Developed a pedometer system comprising an ADXL345 accelerometer sensor module, STM32F103C8T6 microcontroller, and LCD1602 display module
- The system captures three-axis acceleration data from human movement and calculates step count in real-time

---

## Athletic Achievements

**Competitive Soccer Player** | Main Winger Position

- **2nd Place** - Shaoxing City College Student Football League
- **6th Place** - Zhejiang Province College Student Football League
- **Participant** - Zhejiang Province College Student Sports Games (Football)

---

## Technical Skills

**Programming Languages:** Java, Python, Go, C/C++, TypeScript, JavaScript, HTML/CSS, SQL

**Web Frameworks:** Spring Boot, Flask, Next.js, React.js, Angular

**Message Queues:** Kafka, RocketMQ, RabbitMQ

**Databases & Caching:** PostgreSQL, MySQL, neo4j, MongoDB, Redis

**Testing:** JUnit, Mockito, pytest

**DevOps & Cloud:** Docker, Kubernetes, AWS, Jenkins, Nginx, GitHub Actions, Azure DevOps, CI/CD Pipelines

**Search & Analytics:** Elasticsearch, Lucene

**AI/ML Frameworks:** PyTorch, TensorFlow

**Data Analysis & Statistics:** Pandas, NumPy, R, MATLAB, Scikit-learn

---

## Get in Touch

Feel free to reach out to discuss technology, collaborate on projects, or just chat about software engineering and machine learning!

