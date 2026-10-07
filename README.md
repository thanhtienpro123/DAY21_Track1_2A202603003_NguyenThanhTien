# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: Nguyễn Thanh Tiến
- MSSV / mã học viên: 2A202603003
- Lớp: Track 1
- Ngành đã chọn: Giáo dục / AI hỗ trợ học tập và đánh giá

## 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | AI có thể giải thích sai kiến thức, tạo nguồn không tồn tại, đưa phản hồi thiên lệch hoặc khiến giáo viên kết luận sai về năng lực và tính trung thực của người học. Người học có thể mất điểm, cơ hội học tập, quyền riêng tư hoặc niềm tin vào nhà trường. |
| Mức độ high-stakes | Cao đối với chấm điểm, kỷ luật học vụ, tuyển sinh và quyết định ảnh hưởng tốt nghiệp; trung bình đối với gợi ý ôn tập không dùng để chấm. Sai sót có thể ảnh hưởng trực tiếp đến cơ hội học tập và hồ sơ của người học. |
| Dữ liệu nhạy cảm có thể được sử dụng | Bài làm, lịch sử học tập, điểm số, thông tin định danh, ngôn ngữ mẹ đẻ, dữ liệu khuyết tật hoặc nhu cầu hỗ trợ. Không đưa dữ liệu cá nhân thật vào công cụ công khai. |
| Nhu cầu human review | Cao khi AI tham gia chấm điểm, phát hiện gian lận, kỷ luật hoặc đưa ra nội dung liên quan đến sức khỏe/an toàn. Giáo viên cần kiểm tra bằng chứng gốc, cho người học quyền giải trình và không dùng điểm detector làm căn cứ duy nhất. Với gợi ý ôn tập ít rủi ro, người học vẫn cần kiểm tra đáp án và nguồn. |

## 2. Case study 1 — Detector gắn nhãn sai bài viết của người học tiếng Anh

### Brief Case

- Tổ chức / sản phẩm AI: Nghiên cứu của Liang và cộng sự đánh giá 7 công cụ phát hiện văn bản do GPT tạo ra; đây là đánh giá nhiều detector, không phải tuyên bố về một sản phẩm duy nhất.
- Thời gian, địa điểm / bối cảnh: Nghiên cứu công bố trên arXiv ngày 6/4/2023; khảo sát khả năng phân biệt bài viết người và AI, trong đó có bài TOEFL của người học tiếng Anh không phải bản ngữ.
- AI được dùng để làm gì: Detector được quảng bá để nhận diện nội dung do AI tạo, có thể được giáo viên dùng để rà soát nghi vấn gian lận trong bài viết.
- Vấn đề hoặc sự kiện đáng chú ý: Trong bộ 91 bài TOEFL của người học không phải bản ngữ, detector thường xuyên phân loại nhầm bài do người viết thành văn bản AI. Đây là false positive trong bối cảnh có thể dẫn đến cáo buộc gian lận.
- Số liệu có nguồn: Trong 91 bài TOEFL, trung bình 61,22% bị phân loại là do AI tạo; 89/91 bài (97%) bị ít nhất một trong 7 detector gắn cờ, và 18/91 bài (19%) bị cả 7 detector cùng gắn cờ. Đây là kết quả trên tập bài được nghiên cứu, không phải tỷ lệ áp dụng được cho mọi người học hay mọi detector.
- Nguồn: Weixin Liang, Mert Yuksekgonul, Yining Mao, Eric Wu và James Zou, “GPT detectors are biased against non-native English writers”, arXiv:2304.02819, bản nộp ngày 6/4/2023, https://arxiv.org/abs/2304.02819; Andrew Myers, Stanford HAI, “AI-Detectors Biased Against Non-Native English Writers”, 15/5/2023, https://hai.stanford.edu/news/ai-detectors-biased-against-non-native-english-writers.
- Phân biệt bằng chứng và nhận định: Nghiên cứu xác nhận các detector được thử nghiệm gắn cờ nhầm bài TOEFL trong tập dữ liệu nêu trên. Việc một trường dùng detector và xử phạt người học có thể gây mất điểm hoặc cơ hội là phân tích nguy cơ; nghiên cứu này không chứng minh một trường cụ thể đã xử phạt các tác giả của 91 bài.

### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Giáo viên nhận cảnh báo detector rồi quyết định mở điều tra, cho điểm 0 hoặc chuyển vụ việc thành cáo buộc gian lận. |
| Stakeholder bị ảnh hưởng | Người học tiếng Anh không phải bản ngữ có bài viết bị gắn cờ; giáo viên và nhà trường cũng chịu ảnh hưởng khi phải giải quyết khiếu nại hoặc đưa ra quyết định thiếu căn cứ. |
| Failure mode | Bias / fairness và false positive; người viết có cách dùng từ hoặc cấu trúc câu ít đa dạng hơn có nguy cơ bị nhận diện sai trong bộ dữ liệu của nghiên cứu. |
| Layer bắt đầu lỗi | Model / cách đánh giá detector. Nghiên cứu liên hệ lỗi với các đặc trưng như perplexity; không đủ bằng chứng để xác định cấu hình UX hay quy trình của từng trường. |
| Harm xảy ra là gì? | Nghiên cứu chứng minh lỗi phân loại trong tập mẫu. Mất điểm, bị kỷ luật hoặc tổn hại danh dự là hậu quả có thể xảy ra nếu trường xem kết quả detector như bằng chứng kết luận; không khẳng định các hậu quả đó đã xảy ra với 91 người viết. |
| Harm lens | Opportunity loss (nguy cơ mất điểm/cơ hội học tập) và dignity loss (nguy cơ bị nghi ngờ thiếu công bằng). |
| Severity | High nếu cảnh báo sai dẫn tới kỷ luật hoặc ảnh hưởng tốt nghiệp; Medium nếu chỉ kích hoạt bước rà soát có quyền giải trình. Đây là đánh giá theo hậu quả, không phải kết luận của nghiên cứu. |
| Scale | Trong bộ mẫu: 89/91 bài bị ít nhất một detector gắn cờ. Không suy rộng con số này thành tỷ lệ của toàn bộ người học hoặc mọi hệ thống. |
| Probability | Cao trong điều kiện gần với nhóm bài TOEFL và các detector được thử nghiệm; chưa đủ dữ liệu để ước lượng xác suất trong một trường hay hệ thống khác. |
| Frequency | Detector có thể lặp lại cảnh báo ở mỗi lần chấm bài nếu trường dùng nó thường xuyên; tần suất sử dụng thực tế không được đo trong nghiên cứu. |
| Vì sao? | Các tỷ lệ false positive là số liệu của nghiên cứu trên một tập 91 bài và 7 detector. Mức severity phụ thuộc quy trình của trường: cảnh báo chỉ để tham khảo khác với quyết định xử phạt tự động. |

## 3. Case study 2 — ChatGPT bị dùng để kết luận bài tập của sinh viên tại Texas A&M-Commerce

### Brief Case

- Tổ chức / sản phẩm AI: ChatGPT của OpenAI, được một giảng viên tại Texas A&M University-Commerce dùng để kiểm tra bài tập của sinh viên.
- Thời gian, địa điểm / bối cảnh: Sự việc được báo cáo ngày 15/5/2023 tại Texas A&M University-Commerce, Hoa Kỳ; lớp có sinh viên năm cuối ngành khoa học nông nghiệp và tài nguyên thiên nhiên.
- AI được dùng để làm gì: Giảng viên dán bài làm vào ChatGPT và hỏi chatbot có tạo ra văn bản đó hay không, rồi dùng phản hồi làm căn cứ nghi ngờ bài do AI viết.
- Vấn đề hoặc sự kiện đáng chú ý: ChatGPT không phải công cụ xác minh quyền tác giả. Hệ thống có thể tạo ra lời khẳng định sai rằng nó đã viết một đoạn văn. Giảng viên nói các bài bị cả hai lượt kiểm tra nhận là AI sẽ bị điểm 0; sau đó nhà trường cho biết không sinh viên nào trượt môn hoặc bị cấm tốt nghiệp vì sự việc.
- Số liệu có nguồn: Theo Business Insider, giảng viên đưa ba bài tập cuối của sinh viên vào ChatGPT và kiểm tra mỗi bài hai lần; bài báo mô tả ban đầu rằng hơn một nửa lớp bị đánh trượt. Tuy nhiên, tuyên bố của trường được bài báo trích dẫn nói không sinh viên nào trượt môn hoặc bị ngăn tốt nghiệp vì sự việc. Không có số sĩ số lớp được xác nhận trong các nguồn dưới đây, nên không suy ra số sinh viên cụ thể.
- Nguồn: Sophia Ankel, Business Insider, “A Texas professor failed more than half of his class after ChatGPT falsely claimed it wrote their papers”, 17/5/2023, https://www.businessinsider.com/professor-fails-students-after-chatgpt-falsely-said-it-wrote-papers-2023-5; AI Incident Database, “Incident 538: Texas A&M-Commerce Professor Reportedly Used ChatGPT to Accuse Students of Cheating and Assign Incomplete Grades”, sự việc ngày 15/5/2023, https://incidentdatabase.ai/cite/538/.
- Phân biệt bằng chứng và nhận định: Business Insider thuật lại email và cách giảng viên kiểm tra bài, đồng thời dẫn phản hồi chính thức của trường rằng không sinh viên nào trượt hoặc bị cấm tốt nghiệp vì việc này. Tiêu đề báo nói “hơn một nửa lớp bị đánh trượt”, nên cần đọc cùng lời đính chính của trường; không coi số sinh viên bị trượt hoặc mất bằng là hậu quả đã xác nhận. Rủi ro về hoang mang, mất thời gian và nguy cơ bị đánh giá oan là phân tích dựa trên sự việc.

### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Giảng viên nhận câu trả lời tự nhận quyền tác giả từ ChatGPT rồi quyết định cho điểm 0, ghi incomplete hoặc xử lý kỷ luật sinh viên. |
| Stakeholder bị ảnh hưởng | Sinh viên năm cuối có bài bị nghi ngờ; giảng viên phải giải quyết phản hồi và nhà trường chịu trách nhiệm về tính công bằng của đánh giá học vụ. |
| Failure mode | Hallucination: chatbot khẳng định sai rằng nó đã viết văn bản. Over-reliance: người dùng xem câu trả lời đó như bằng chứng xác minh thay vì một đầu ra không đáng tin cho mục đích nhận diện tác giả. |
| Layer bắt đầu lỗi | UX / quy trình sử dụng: ChatGPT bị dùng ngoài mục đích để xác minh tác giả, rồi đầu ra được gắn với quyết định chấm điểm. Model cũng tạo câu trả lời sai, nhưng nguồn không cho phép xác định kỹ thuật hay cơ chế nội bộ nào gây ra câu trả lời đó. |
| Harm xảy ra là gì? | Nguồn xác nhận có cáo buộc và việc giảng viên dự định cho điểm 0/incomplete dựa trên cách kiểm tra này; trường nói không sinh viên nào trượt môn hay bị cấm tốt nghiệp vì sự việc. Lo lắng, thời gian khiếu nại và nguy cơ ảnh hưởng học vụ là harm được báo cáo hoặc suy luận; không khẳng định sinh viên cuối cùng mất bằng. |
| Harm lens | Opportunity loss (nguy cơ mất điểm hoặc chậm hoàn tất học vụ) và dignity loss (bị nghi gian lận thiếu căn cứ). |
| Severity | High ở thời điểm quyết định vì điểm 0/incomplete có thể ảnh hưởng tốt nghiệp; hậu quả cuối cùng được trường xác nhận là không có sinh viên trượt hoặc bị cấm tốt nghiệp do sự việc. |
| Scale | Một lớp sinh viên năm cuối; bài báo nói “hơn một nửa lớp” ở tiêu đề nhưng không nêu sĩ số xác nhận và trường phủ nhận có sinh viên trượt do việc này. Không quy đổi thành số người cụ thể. |
| Probability | Cao trong chính tình huống được báo cáo: ChatGPT đã trả lời sai về quyền tác giả và phản hồi đó được dùng làm căn cứ. Không đủ dữ liệu để ước lượng xác suất cho các lớp hoặc phiên bản ChatGPT khác. |
| Frequency | Giảng viên báo cáo đã kiểm tra ba bài cuối, mỗi bài hai lần. Đây là số lượt kiểm tra được tường thuật, không chứng minh ChatGPT luôn đưa ra cùng câu trả lời hoặc lỗi phổ biến ở quy mô lớn. |
| Vì sao? | Số liệu về ba bài và hai lượt kiểm tra được Business Insider tường thuật. Cần giữ riêng mô tả ban đầu của báo chí với tuyên bố chính thức của trường; kết quả thực tế cho thấy nguy cơ học vụ nghiêm trọng nhưng không xác nhận có sinh viên bị chặn tốt nghiệp. |

## 4. Nhận xét và biện pháp giảm thiểu

Hai case cho thấy rủi ro giáo dục không chỉ đến từ độ tin cậy của công cụ mà còn từ cách tổ chức sử dụng kết quả. Detector và chatbot không nên là bằng chứng duy nhất để buộc tội người học; nhà trường cần cho phép giải trình, xem bản nháp/lịch sử làm bài khi phù hợp và đánh giá bằng nhiều nguồn bằng chứng. Với GenAI nói chung, cơ sở giáo dục nên công bố quy tắc sử dụng, giới hạn dữ liệu được nhập, yêu cầu kiểm chứng nguồn và xác định rõ người chịu trách nhiệm cuối cùng. Các bước này là đề xuất giảm thiểu của tôi, không phải kết quả thực nghiệm của hai nguồn trên.

## 5. Giới hạn và ghi chú

- Case 1 là nghiên cứu đánh giá detector trên một mẫu bài viết cụ thể; kết quả không thể khái quát tự động sang mọi ngôn ngữ, công cụ hoặc nhóm người học.
- Case 2 là một sự cố đơn lẻ được báo chí tường thuật; phản hồi của trường khác với tiêu đề ban đầu về việc sinh viên có trượt môn hay bị giữ bằng. Harm Map giữ rõ sự khác biệt giữa cáo buộc, hậu quả được báo cáo và kết quả nhà trường xác nhận.
- Các mức Severity, Scale, Probability và Frequency là đánh giá định tính của tôi theo dữ liệu hiện có; nơi thiếu dữ liệu đã ghi rõ thay vì tự đặt tỷ lệ.
- Nguồn chính và số liệu cần được mở kiểm tra lại trước khi nộp; nếu giảng viên yêu cầu case là một sự cố sản phẩm cụ thể thay vì nghiên cứu/khảo sát, cần thay Case 2 bằng sự cố có tài liệu nguồn xác nhận.

