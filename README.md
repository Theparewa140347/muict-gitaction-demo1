# ใช้ Python เวอร์ชัน 3.11-slim จาก DockerHub
FROM python:3.11-slim

# กำหนดโฟลเดอร์ทำงานใน container
WORKDIR /app

# คัดลอกไฟล์ requirements.txt ไปยัง container
COPY requirements.txt .

# ติดตั้ง dependencies จากไฟล์ requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# คัดลอกแอป FastAPI ทั้งหมดไปยัง container
COPY . .

# เปิดพอร์ต 8000 ให้เข้าถึงได้จากภายนอก
EXPOSE 8000

# รันแอป FastAPI ด้วย Uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
