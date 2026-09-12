# Quy tắc quản trị AI_Space

## 1. Nguồn chuẩn và nguyên tắc chung

- Gọi người dùng là anh Hưng.
- Phạm vi Google Drive mặc định để tạo file mới là **My Drive** của tài khoản `xuanhungngo@gmail.com` đang kết nối. Chỉ số `/u/0/`, `/u/1/` trên URL là vị trí tài khoản trong trình duyệt, không phải định danh kho.
- Không dùng folder ID `1rZQvJNOKSN9Ym7A8NwqMhw-gaP9ftVJB` làm nơi tạo file mặc định, nơi dự phòng hoặc nơi tự động gom file. Chỉ ghi vào folder này khi anh Hưng chỉ định rõ cho một nhiệm vụ cụ thể.
- Root AI_Space chính thức là Google Drive folder ID `1WmAJH_H-VEXWrcuS-VJf2Xmr7Ov0TVQ_` (`https://drive.google.com/drive/folders/1WmAJH_H-VEXWrcuS-VJf2Xmr7Ov0TVQ_`).
- Dùng folder ID làm định danh; không chọn thư mục khác chỉ vì trùng tên và không suy ra đường dẫn `G:` từ URL.
- Với artifact thuộc AI_Space, bắt đầu từ My Drive rồi định tuyến vào đúng thư mục con dưới AI_Space; không để file rời ở root My Drive nếu đã xác định được đích theo cây AI_Space.
- Làm việc cloud-first trong phạm vi công cụ và quyền thực sự được hỗ trợ.
- Google Drive là nơi lưu tài liệu và artifact đã được chỉ định; GitHub là nguồn chuẩn của code khi đã có repository; runtime phải có persistence thật cho state sống.
- Không giữ hai bản cùng là nguồn chuẩn hoặc hai bản editable được sửa song song.
- Không lưu secret, credential hoặc token trong AI_Space, repository, gói phát hành hay tài liệu hướng dẫn.

## 2. Cây thư mục AI_Space đã duyệt

| Đường dẫn | Nội dung |
|---|---|
| `00_Registry/repositories/` | Danh mục repository và nguồn code |
| `00_Registry/deployments/` | Phiên bản đang cài hoặc triển khai |
| `00_Registry/storage/` | Ánh xạ kho dữ liệu và folder ID |
| `01_Development/incoming/` | Source chưa có repository |
| `01_Development/projects/` | Cloud Workspace cho sản phẩm phần mềm dùng lại; hồ sơ phát triển, audit và bàn giao |
| `01_Development/releases/` | Gói phát hành sinh từ phiên bản xác định |
| `02_Workspace/projects/` | Cloud Workspace cho project ChatGPT/Codex thông thường và workspace viết báo cáo theo dự án/giai đoạn |
| `02_Workspace/tasks/` | Công việc AI không thuộc một báo cáo dự án |
| `03_Knowledge/xh-tuvan/` | Tiếp nhận, bằng chứng, đánh giá và projection bài học chung |
| `03_Knowledge/global-control/operational/` | Bằng chứng vận hành điều phối |
| `04_Library/templates/` | Mẫu dùng lại |
| `04_Library/references/` | Tài liệu tham khảo dùng chung |
| `04_Library/tools/` | Công cụ dùng độc lập hoặc bản dùng của công cụ |
| `04_Library/artifacts/` | Artifact tái sử dụng |
| `05_Docs/architecture/` | Kiến trúc đã chốt |
| `05_Docs/guides/` | Hướng dẫn dùng lâu dài |
| `05_Docs/prompts/` | Prompt dùng lại hoặc chuyển phiên |
| `05_Docs/decisions/` | Quyết định đã chốt |
| `06_Platforms/claude/` | Instruction, cấu hình mẫu và handoff riêng Claude |
| `06_Platforms/chatgpt/` | Instruction, cấu hình mẫu và handoff riêng ChatGPT |
| `90_Archive/` | Bản cũ đã xác minh; không tự xóa |

Chỉ tạo thư mục con khi có nội dung. Không sao chép policy của Global Control vào Registry.

## 3. Source, plugin, skill, MCP và công cụ

- Trước khi có repository, đặt source đang chuẩn bị tại `01_Development/incoming/<name>/`.
- Sau khi có repository, dùng GitHub làm nguồn chuẩn. Checkout trong executor chỉ là bản làm việc; không sửa song song source trên Drive.
- Giữ `xh-tuvan` và `xh-global-control` thành hai repository độc lập. Dùng chung logic nghiệp vụ giữa Claude và ChatGPT; chỉ tách manifest hoặc adapter theo nền tảng khi cần.
- Với project phát triển plugin `xh-tuvan`, dùng `01_Development/projects/xh-tuvan/` làm Cloud Workspace cho hồ sơ phát triển, audit, quyết định và handoff. Source canonical vẫn ở repository GitHub khi repository đã tồn tại; gói phát hành ở `01_Development/releases/xh-tuvan/<version>/`; bản cài runtime ở vị trí do ứng dụng quản lý. Không dùng `02_Workspace/projects/xh-tuvan/` làm nguồn code song song.
- Mỗi dự án báo cáo mà `xh-tuvan` phục vụ là một project nghiệp vụ riêng tại `02_Workspace/projects/<project-code>/<report-or-stage>/`; không đặt hồ sơ dự án khách hàng vào workspace phát triển plugin.
- Đặt source của MCP hoặc công cụ dùng chung trong repository riêng khi chúng có vòng đời độc lập; không nhét vào Global Control chỉ vì được nhiều AI sử dụng.
- Đặt gói ZIP phát hành tại `01_Development/releases/<name>/<version>/` và ghi rõ tag hoặc commit nguồn.
- Đặt bản công cụ độc lập dùng hằng ngày tại `04_Library/tools/<name>/`; dẫn về repository nếu có source.
- Skill phải được tạo, kiểm tra và cài bằng cơ chế quản lý skill được hỗ trợ. File Markdown trên Drive hoặc URL GitHub không tự làm skill có hiệu lực.
- Plugin và MCP phải được cài, triển khai hoặc kết nối; nhìn thấy source không chứng minh chúng đang chạy.
- Cập nhật Registry sau khi phiên bản cài hoặc triển khai thay đổi.

## 4. Cloud Workspace cho project ChatGPT/Codex và workspace báo cáo

### 4.1. Quy tắc tạo Cloud Workspace đồng hành

- Khi tạo một project ChatGPT hoặc Codex mới có mục tiêu làm việc lâu dài, đồng thời tạo hoặc liên kết một Cloud Workspace dưới root AI_Space canonical.
- Project thông thường đặt tại `02_Workspace/projects/<project-code>/`.
- Project phát triển một sản phẩm phần mềm dùng lại như skill, plugin, MCP server hoặc `xh-tuvan` đặt tại `01_Development/projects/<product-name>/`; quy tắc này không biến Drive thành nguồn code canonical khi đã có repository.
- Trao đổi ngắn hoặc task không cần lưu bền vững không bắt buộc tạo project workspace; nếu cần artifact bền vững nhưng không thuộc project, dùng `02_Workspace/tasks/<task-code>/`.
- Cloud Workspace và project native trong ChatGPT/Codex là hai đối tượng khác nhau. `project.json` phải ghi tối thiểu loại project, nền tảng, native project ID hoặc URL khi lấy được, Drive folder ID, nguồn canonical và thời điểm tạo/cập nhật.
- Claude và ChatGPT/Codex được dùng chung Cloud Workspace cho cùng một project. Dùng một writer cho cùng state hoặc artifact; không tạo hai bản editable theo nền tảng.

### 4.2. Cấu trúc workspace báo cáo

Dùng cấu trúc:

```text
02_Workspace/projects/<project-code>/<report-or-stage>/
├── README.md
├── project.json
├── 10_Sources/
│   ├── 10_User_Input/
│   └── 20_Source_Snapshots/
├── 20_Templates/
├── 30_Working/
│   ├── 10_Research/
│   ├── 20_Evidence/
│   ├── 30_Specs/
│   ├── 40_Drafts/
│   ├── 50_Reviews/
│   ├── 60_Edit_Analysis/
│   ├── 70_Learning_Candidates/
│   ├── .ai/
│   └── .xh/
├── 40_Outputs/
└── 50_Feedback/
```

- `README.md` là chỉ mục dễ đọc, không phải state thứ hai.
- `project.json` lưu identity, metadata, source references và cấu hình.
- Hai nguồn input gồm: kho dự án hoặc Drive ngoài workspace được chỉ định, mặc định chỉ đọc; và input riêng trong `10_Sources/10_User_Input/`.
- Chỉ snapshot nguồn cần dùng. Ghi ID hoặc URL, revision, `modifiedTime` hay hash khi có.
- Không tự sửa, di chuyển, xóa hoặc nhập toàn bộ kho dự án nguồn. Yêu cầu xác minh khi nguồn mâu thuẫn.
- Workspace là công đoạn viết báo cáo, không phải kho hồ sơ nộp chủ đầu tư và không quản lý tính toán hoặc dự toán dự án.
- Có thể dùng kết quả tính toán sẵn có làm input. Không tạo `calculations/` cho workspace mới; bảo toàn thư mục cũ khi migration.
- Mỗi báo cáo hoặc giai đoạn dùng workspace riêng và không lẫn state.

### 4.3. Phân vùng dùng chung và riêng nền tảng

- `00_Registry` đến `05_Docs` và `90_Archive` là vùng dùng chung cho Claude và ChatGPT/Codex theo đúng chức năng từng thư mục.
- `06_Platforms/claude/` chỉ lưu instruction, cấu hình mẫu và handoff riêng Claude.
- `06_Platforms/chatgpt/` chỉ lưu instruction, cấu hình mẫu và handoff riêng ChatGPT/Codex. Folder ID `1lSJnvOt8Kj_fzOjVKS77JVnCQIuHGtDV` chính là vùng `06_Platforms/chatgpt/`; không dùng nơi này cho source, release hoặc workspace dự án.
- Quy tắc, kiến trúc, tài liệu và tri thức dùng chung phải đặt ở vùng chung tương ứng; không sao chép sang cả hai nhánh nền tảng.

## 5. Hợp đồng Outputs–Feedback

- Với mỗi báo cáo xuất cho anh Hưng rà soát, tạo một baseline trong `40_Outputs/` và một bản byte-identical có hậu tố `_XHedited` trong `50_Feedback/`.
- Ví dụ: `40_Outputs/BC-NCKT_BTU-4TB_R01.docx` và `50_Feedback/BC-NCKT_BTU-4TB_R01_XHedited.docx`.
- Giữ baseline Output bất biến. Không ghi đè Feedback đã tồn tại.
- Tạo cặp mới bằng revision `R01`, `R02`, `R03`...; không dùng tên `final-final`.
- Lần chạy lại cùng revision phải idempotent hoặc báo xung đột.
- Theo dõi cặp bằng ID, revision, hash, thời điểm và phiên bản plugin.
- Chỉ phân tích sau khi anh Hưng báo sửa xong hoặc yêu cầu học; không tự học file đang được chỉnh sửa.
- So sánh đúng baseline, bảo toàn cấu trúc Word, bảng và hình; phân biệt thay đổi nội dung với thay đổi định dạng.
- Không tạo Feedback hàng loạt cho file Markdown nội bộ, log, ảnh preview hay file kỹ thuật.

## 6. Knowledge và phân ranh hệ thống

- Đặt phản hồi riêng của dự án trong workspace. Đưa đề xuất có khả năng dùng lại vào kho chung kèm nguồn gốc và bằng chứng.
- Luồng bài học chung: `inbox` → `evidence` → `review` → cập nhật tri thức versioned trong repository `xh-tuvan` → projection chỉ đọc tại `published`.
- Không sửa tay `published` và không tự phê duyệt bài học.
- Hermes phụ trách hạ tầng và gateway.
- Global Control phụ trách policy, routing, budget, session, worker và cơ chế state.
- `xh-tuvan` phụ trách nghiệp vụ viết báo cáo, quản lý nguồn, QA và learning chuyên ngành.
- Không mở SQLite đang sống trên Drive sync. Không giả định file MD hoặc JSON có thể phục hồi đầy đủ lịch sử revision và approval.

## 7. Quy tắc thao tác và bàn giao

- Đọc Registry và context đúng nhiệm vụ; không quét toàn bộ Drive nếu không cần.
- Chọn workspace theo loại project, project ID và report hoặc stage. Project thông thường dùng `02_Workspace/projects`; sản phẩm phần mềm dùng lại dùng `01_Development/projects`; nếu không xác định được từ inventory, hỏi đúng phần còn thiếu và không tự tạo dự án trùng.
- Không ép đổi cây workspace cũ trước khi migration và kiểm thử tương thích hoàn tất.
- Dùng một writer cho cùng state hoặc artifact. Khi revision đã thay đổi, refresh và reconcile trước khi ghi.
- Tài liệu hỏi đáp dùng lại đặt tại `05_Docs/guides/` hoặc `05_Docs/prompts/`; ghi chú nhiệm vụ đặt trong workspace; cấu hình riêng nền tảng đặt dưới `06_Platforms/<platform>/`.
- Nội dung trao đổi ngắn không cần tạo file.
- Chuyển output sang kho hồ sơ nộp chủ đầu tư là tác vụ riêng, cần yêu cầu và đích cụ thể.
- Nếu connector không ghi được Drive, lưu tại nơi bền vững được môi trường hỗ trợ, cung cấp artifact và nói rõ chưa đồng bộ; không tuyên bố đã lưu vào Drive.
- Trước mỗi lần tạo file trên Drive, xác minh tài khoản, parent folder và folder ID đích. Nếu công cụ chỉ cung cấp một thư mục mặc định không phải My Drive hoặc AI_Space đã duyệt, dừng ghi và báo anh Hưng thay vì âm thầm dùng thư mục đó.
- Kết thúc phiên, ghi handoff hoặc state bằng cơ chế được hỗ trợ, gồm output ID, tiến độ, vấn đề và bước tiếp theo.
- Khi phiên dài, chuẩn bị prompt chuyển phiên gồm trạng thái, quyết định, giả định và bước tiếp; không tuyên bố biết chính xác token còn lại.
