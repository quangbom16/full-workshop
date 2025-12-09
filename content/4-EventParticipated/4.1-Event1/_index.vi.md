---
title: "Sự kiện: Workshop AI/ML/GenAI trên AWS"
date: "2025-11-15"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

## Báo cáo tổng kết: "Workshop AI/ML/GenAI trên AWS"

### Mục tiêu sự kiện

- Cung cấp cái nhìn tổng quan toàn diện về bối cảnh AI/ML đặc biệt tại thị trường Việt Nam.
- Đi sâu vào Amazon SageMaker để quản lý vòng đời máy học (Machine Learning) toàn diện.
- Khám phá các khả năng Generative AI (AI tạo sinh) nâng cao sử dụng Amazon Bedrock.
- Làm chủ các kỹ thuật hiện đại như RAG (Retrieval-Augmented Generation) và Kỹ thuật gợi ý (Prompt Engineering).
- Tạo điều kiện học tập thực hành thông qua các bản demo trực tiếp về SageMaker Studio và xây dựng GenAI chatbot.

### Diễn giả

- **Kha Van** – AWS Community Leader và Host của Workshop

### Điểm nổi bật chính

#### Hiểu về bối cảnh AI/ML tại Việt Nam

- Tổng quan về tình hình áp dụng AI hiện tại ở Việt Nam.
- Các hoạt động giao lưu (networking) và làm quen để kết nối với đồng nghiệp trong nước.
- Thảo luận về xu hướng thị trường địa phương, cơ hội và thách thức khi triển khai AI.

#### Amazon SageMaker – Nền tảng ML toàn diện (End-to-End)

**Chuẩn bị và Gán nhãn dữ liệu**
- Các chiến lược thu thập dữ liệu hiệu quả.
- Công cụ gán nhãn tập dữ liệu để chuẩn bị cho học có giám sát (supervised learning).
- Quy trình tiền xử lý để đảm bảo chất lượng dữ liệu.

**Huấn luyện, Tinh chỉnh và Triển khai mô hình**
- Sử dụng các thuật toán có sẵn so với việc dùng custom scripts.
- Tinh chỉnh siêu tham số (Hyperparameter tuning) để tối ưu hóa hiệu suất mô hình.
- Các chiến lược triển khai cho môi trường sản xuất (production).

**Các khả năng MLOps tích hợp**
- Triển khai CI/CD cho Machine Learning.
- Tự động hóa các pipeline để giảm thiểu sự can thiệp thủ công.
- Giám sát hiệu suất mô hình trong môi trường thực tế.

**Demo trực tiếp: Hướng dẫn sử dụng SageMaker Studio**
- Điều hướng trên IDE thống nhất dành cho phát triển ML.
- Trực quan hóa quy trình làm việc từ dữ liệu đến triển khai.

#### Generative AI với Amazon Bedrock

**Các mô hình nền tảng (Foundation Models - FMs)**
- So sánh và hướng dẫn lựa chọn các mô hình hàng đầu: **Claude, Llama, và Titan**.
- Hiểu về sự đánh đổi giữa hiệu năng, chi phí và độ trễ.

**Kỹ thuật Prompt Engineering**
- Các thực hành tốt nhất để tương tác với LLMs.
- Các kỹ thuật nâng cao: **Chain-of-Thought (CoT)** reasoning và **Few-shot learning** để cải thiện độ chính xác của mô hình.

**Retrieval-Augmented Generation (RAG)**
- Phân tích kiến trúc: Kết nối LLMs với các nguồn dữ liệu bên ngoài.
- Tích hợp với Knowledge Bases để giảm thiểu ảo giác (hallucinations) và cung cấp thông tin cập nhật.

**Bedrock Agents & Guardrails**
- **Agents**: Tạo các quy trình công việc nhiều bước và tích hợp với các công cụ/API bên ngoài để thực hiện tác vụ.
- **Guardrails**: Triển khai các bộ lọc an toàn và kiểm duyệt nội dung để đảm bảo sử dụng AI có trách nhiệm.

**Demo trực tiếp: Xây dựng Generative AI Chatbot**
- Hướng dẫn từng bước xây dựng một chatbot hoạt động được sử dụng Amazon Bedrock.

### Bài học chính (Key Takeaways)

#### Chiến lược ML & GenAI

- **Lựa chọn mô hình là quan trọng**: Việc chọn đúng Mô hình nền tảng (Claude vs. Llama vs. Titan) phụ thuộc nhiều vào trường hợp sử dụng cụ thể và ngân sách.
- **RAG là thiết yếu**: Đối với các ứng dụng doanh nghiệp, RAG là yếu tố cốt lõi để cung cấp các phản hồi chính xác, nhận biết ngữ cảnh dựa trên dữ liệu nội bộ.
- **An toàn là trên hết**: Việc triển khai Guardrails là không thể thương lượng đối với các ứng dụng GenAI thực tế để ngăn chặn nội dung độc hại.

#### Kiến trúc kỹ thuật

- **SageMaker là trung tâm**: Đóng vai trò là hệ thần kinh trung ương cho các mô hình ML truyền thống (Predictive AI).
- **Bedrock là lớp GenAI**: Cung cấp một lớp trừu tượng dạng serverless, dựa trên API để truy cập các FMs mạnh mẽ mà không cần quản lý hạ tầng.
- **Agents để hành động**: Chuyển từ việc chỉ tạo văn bản đơn thuần sang thực thi các tác vụ (gọi API, tra cứu dữ liệu) bằng Bedrock Agents.

#### Sự xuất sắc trong vận hành

- **Kỹ năng Prompt Engineering**: Đây là năng lực quan trọng đối với các lập trình viên để khai thác hiệu suất tốt nhất từ LLMs.
- **MLOps**: Tích hợp và triển khai liên tục là yếu tố sống còn để duy trì tính phù hợp và hiệu suất của mô hình theo thời gian.

### Ứng dụng vào công việc

- **Triển khai RAG**: Xây dựng các công cụ tìm kiếm tri thức nội bộ sử dụng Amazon Bedrock và Knowledge Bases để giúp nhân viên tìm thông tin nhanh hơn.
- **Phát triển Smart Agents**: Sử dụng Bedrock Agents để tự động hóa các tác vụ chăm sóc khách hàng hoặc quy trình nội bộ.
- **Chuẩn hóa quy trình ML**: Chuyển đổi các thử nghiệm ML rời rạc sang Amazon SageMaker pipelines để quản trị tốt hơn và dễ dàng tái lập.
- **Áp dụng Guardrails**: Rà soát các ứng dụng GenAI hiện tại và áp dụng Bedrock Guardrails để đảm bảo tuân thủ và an toàn.
- **Tối ưu hóa chi phí**: Đánh giá việc sử dụng các Mô hình nền tảng khác nhau để cân bằng giữa khả năng và chi phí.

### Trải nghiệm sự kiện

Tham dự **"Workshop AI/ML/GenAI trên AWS"** là một trải nghiệm mang tính thực tiễn cao và hướng tới tương lai. Buổi học đã kết nối hiệu quả khoảng cách giữa Machine Learning truyền thống và thế giới Generative AI tiên tiến. Những trải nghiệm chính bao gồm:

- Phần **hướng dẫn SageMaker Studio** đã làm rõ cách quản lý vòng đời phức tạp của các mô hình ML trong một giao diện duy nhất.
- Phần đi sâu vào **Amazon Bedrock** đặc biệt giá trị, nhất là sự so sánh giữa các mô hình như **Claude và Llama**, giúp làm rõ khi nào nên sử dụng mô hình nào.
- Học về **Retrieval-Augmented Generation (RAG)** đã thay đổi quan điểm của tôi về cách làm cho LLMs trở nên hữu ích với dữ liệu đặc thù của doanh nghiệp mà không cần huấn luyện lại mô hình.
- Phần về **Bedrock Agents** đã mở ra những khả năng mới để xây dựng các ứng dụng thực sự có thể *hành động*, chứ không chỉ *nói*.

#### Tận dụng các công cụ AI hiện đại
- Khám phá các kỹ thuật **Prompt Engineering** như Chain-of-Thought để cải thiện khả năng suy luận trong phản hồi của AI.
- Khám phá cách **Guardrails** có thể được cấu hình để tự động lọc bỏ nội dung không phù hợp.
- Chứng kiến tốc độ xây dựng một **GenAI Chatbot** trực tiếp, minh chứng cho chu kỳ phát triển nhanh chóng khả thi với các công cụ AWS.

#### Bài học rút ra
- **Ngữ cảnh là Vua (Context is King)**: RAG là cách hiệu quả nhất để đưa kiến thức tổ chức vào AI.
- **Đừng phát minh lại cái bánh xe**: Sử dụng các dịch vụ được quản lý như Bedrock thay vì tự host LLMs trừ khi thực sự cần thiết.
- **Bảo mật & An toàn**: Những yếu tố này cần được thiết kế vào ứng dụng GenAI ngay từ ngày đầu tiên sử dụng Guardrails, không phải là thứ thêm vào sau.

Nhìn chung, workshop đã cung cấp một lộ trình rõ ràng để áp dụng cả ML dự đoán (SageMaker) và AI tạo sinh (Bedrock) trong tổ chức, được hỗ trợ bởi bối cảnh thực tế từ thị trường Việt Nam.