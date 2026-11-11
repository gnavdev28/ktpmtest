TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 1
TÀI LIỆU ÔN TẬP
HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
TS. Nguyễn Thành Trung – Trường Công nghệ thông tin Phenikaa
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Dành cho sinh viên | Phiên bản 2026
LƯU Ý QUAN TRỌNG
Tài liệu này định hướng kiến thức và kỹ năng làm bài. 
Tài liệu không phải đề cương giới hạn
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 2
HƯỚNG DẪN SỬ DỤNG TÀI LIỆU
Mục tiêu: Sau khi ôn tập, sinh viên cần nhận diện đúng dịch vụ AWS theo tình huống; phân biệt 
các khái niệm gần nhau; giải thích được trách nhiệm của AWS và khách hàng; đọc được sơ đồ 
kiến trúc cơ bản; và xử lý các câu trắc nghiệm một hoặc nhiều đáp án.
1. Quy trình ôn tập 3 bước
• Bước 1 - Ôn lại toàn bộ nội dung đã học. Đọc lại Slides Tổng quan của giảng viên, tài liệu 
học tập trên Coursera và tài liệu thực hành trên AWS Academy. Không chỉ ghi nhớ tên dịch 
vụ; cần hiểu mục đích, phạm vi và mối quan hệ giữa các dịch vụ.
• Bước 2 - Làm lại câu hỏi trên Coursera. Đối với mỗi câu sai, ghi rõ vì sao phương án 
đúng phù hợp và vì sao các phương án còn lại không phù hợp. Đây là cách phát hiện các cặp 
khái niệm dễ nhầm.
• Bước 3 - Luyện tập có kiểm soát. Sau khi nắm chắc kiến thức, tham khảo AWS Cloud 
Practitioner Study Notes (CLF-C02). Phần đầu hệ thống hóa kiến thức; phần Practice Exam 
gồm 23 bài luyện có đáp án và giải thích. Chỉ dùng để luyện khả năng vận dụng, không học 
thuộc câu hỏi.
Tài liệu tham khảo trực tuyến: AWS Cloud Practitioner Study Notes (CLF-C02)
2. Cách học 
• Luôn trả lời câu hỏi “dịch vụ này giải quyết vấn đề gì?”. Ví dụ: CloudWatch theo dõi chỉ số 
và trạng thái vận hành; CloudTrail ghi lại hoạt động người dùng và API.
• Xác định phạm vi của thành phần. VPC thuộc một Region; subnet thuộc một Availability 
Zone; Security Group gắn với tài nguyên; Network ACL áp dụng ở mức subnet.
• Tìm từ khóa quyết định trong tình huống. “HTTP/HTTPS và định tuyến theo đường dẫn” 
gợi ý ALB; “TCP/UDP, thông lượng rất cao, IP tĩnh” gợi ý NLB.
• Phân biệt “được quản lý” và “tự quản lý”. Dịch vụ càng được AWS quản lý nhiều thì trách 
nhiệm vận hành của khách hàng càng giảm, nhưng khách hàng vẫn chịu trách nhiệm về dữ 
liệu, quyền truy cập và cấu hình sử dụng.
• Với câu chọn nhiều đáp án, đánh giá độc lập từng phương án. Không dừng lại khi đã thấy 
một phương án đúng; kiểm tra đủ số đáp án được yêu cầu.
4. Phạm vi kiến thức trọng tâm
Chuyên đề Trọng tâm cần nắm
Overview Khái niệm cloud; 5 đặc tính; IaaS/PaaS/SaaS; public/private/hybrid/community; 
ảo hóa; AWS global infrastructure; shared responsibility; Well-Architected.
IAM Root user; IAM user/group/role/policy; MFA; access keys; least privilege; 
policy JSON; logic implicit deny/explicit allow/explicit deny; CloudTrail.
Network Region/AZ; VPC/subnet; CIDR; route table; Internet Gateway; NAT Gateway; 
Security Group; Network ACL; Elastic IP; VPN; Direct Connect; edge location.
Compute, 
Storage, 
Database
EC2/AMI/lifecycle/pricing; Lambda; Beanstalk; S3/EBS/EFS/Instance Store; 
snapshot; RDS/Aurora/DynamoDB; Multi-AZ; DMS.
ELB, Scaling, 
Monitor
Scalability/elasticity/high availability/fault tolerance; ALB/NLB/GWLB/CLB; 
Auto Scaling Group; scaling policy; health check; CloudWatch; CloudTrail.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 3
CHUYÊN ĐỀ 1. OVERVIEW
Mục tiêu: Hiểu bản chất điện toán đám mây, phân biệt mô hình dịch vụ và mô hình triển khai, 
giải thích vai trò của ảo hóa và nhận diện các thành phần cơ bản của hạ tầng AWS.
1.1. Khái niệm và 5 đặc tính cốt lõi
Điện toán đám mây là mô hình cung cấp tài nguyên CNTT dùng chung qua mạng, có thể cấp phát và 
thu hồi nhanh theo nhu cầu, với mức tương tác quản trị tối thiểu. Năm đặc tính cốt lõi cần ghi nhớ:
Đặc tính Ý nghĩa Dấu hiệu trong câu hỏi
On-demand selfservice
Người dùng tự cấp phát tài nguyên khi cần, 
không phải chờ nhà cung cấp xử lý thủ công.
“Tự tạo máy chủ”, “cấp phát 
ngay”, “không cần liên hệ bộ 
phận hạ tầng”.
Broad network 
access
Dịch vụ được truy cập qua mạng bằng cơ chế 
tiêu chuẩn, trên nhiều loại thiết bị.
“Truy cập qua Internet”, 
“laptop/điện thoại/máy trạm”.
Resource pooling Tài nguyên vật lý được dùng chung và phân bổ 
động cho nhiều khách hàng, có cách ly logic.
“Multi-tenant”, “shared pool”, 
“vị trí tài nguyên không cố 
định”.
Rapid elasticity Có thể tăng hoặc giảm tài nguyên nhanh theo 
biến động nhu cầu.
“Tăng đột biến”, “mở 
rộng/thu hẹp tự động”.
Measured service Mức sử dụng được đo đếm để theo dõi và tính 
phí.
“Pay for what you use”, “theo 
giờ/yêu cầu/dung lượng”.
1.2. Front-End và Back-End
Thành phần Mô tả Ví dụ
Front-End Phần người dùng nhìn thấy và tương tác: giao 
diện web, ứng dụng, trình duyệt, công cụ quản 
trị.
AWS Management Console, 
ứng dụng web của khách hàng.
Back-End Hạ tầng và phần mềm phía nhà cung cấp: máy 
chủ, lưu trữ, mạng, ảo hóa, cơ chế quản lý và 
điều phối.
Data center, hypervisor, hệ 
thống lưu trữ, mạng lõi.
1.3. Mô hình dịch vụ: IaaS, PaaS, SaaS
Mô hình Khách hàng tập trung vào Nhà cung cấp quản lý nhiều hơn Ví dụ điển hình
IaaS Hệ điều hành khách, 
middleware, ứng dụng, dữ liệu 
và cấu hình bảo mật.
Phần cứng, mạng vật lý, lưu trữ vật 
lý, lớp ảo hóa.
Amazon EC2.
PaaS Mã nguồn, dữ liệu và cấu hình 
ứng dụng.
Hạ tầng, hệ điều hành, runtime, 
triển khai và một phần 
scaling/monitoring.
AWS Elastic 
Beanstalk.
SaaS Sử dụng và cấu hình chức năng 
của ứng dụng.
Toàn bộ ứng dụng và hạ tầng vận 
hành phía dưới.
Gmail, các ứng 
dụng cộng tác 
trực tuyến.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 4
1.4. Mô hình triển khai
Mô hình Đặc điểm chính Tình huống phù hợp
Public cloud Hạ tầng do nhà cung cấp sở hữu và cung 
cấp cho nhiều khách hàng qua mạng công 
cộng; cách ly logic.
Cần triển khai nhanh, giảm đầu tư 
ban đầu, mở rộng linh hoạt.
Private cloud Hạ tầng dành riêng cho một tổ chức, có thể 
đặt tại chỗ hoặc do bên thứ ba vận hành.
Yêu cầu kiểm soát, quy định hoặc 
tích hợp nội bộ nghiêm ngặt.
Hybrid cloud Kết hợp private/on-premises với public 
cloud và có cơ chế trao đổi dữ liệu hoặc 
khối lượng công việc.
Giữ dữ liệu nhạy cảm tại chỗ 
nhưng tận dụng cloud khi cần mở 
rộng.
Community 
cloud
Hạ tầng dùng chung cho một cộng đồng có 
yêu cầu hoặc mục tiêu chung.
Nhóm cơ quan/tổ chức cùng ngành 
có yêu cầu tuân thủ tương tự.
1.5. Ảo hóa và Machine Image
Ảo hóa cho phép nhiều máy ảo sử dụng chung tài nguyên của một máy chủ vật lý trong khi vẫn hoạt 
động như các hệ thống độc lập. Hypervisor/VMM quản lý CPU, bộ nhớ, thiết bị và mức cách ly giữa 
các máy ảo.
Cách gọi trong tài 
liệu học
Thuật ngữ tương 
đương thường gặp Đặc điểm
Hypervisor-based Bare-metal/Type 1 Hypervisor tương tác trực tiếp với phần cứng; 
hiệu năng và cách ly tốt.
Host-based Hosted/Type 2 Lớp ảo hóa chạy trên hệ điều hành máy chủ.
Hybrid Kiến trúc kết hợp Một phần chức năng ảo hóa phối hợp với hệ điều 
hành máy chủ và chế độ đặc quyền.
AMI (Amazon Machine Image): mẫu dùng để khởi chạy EC2 instance, bao gồm thông tin hệ điều 
hành và cấu hình phần mềm cần thiết. AMI không phải là ảnh chụp màn hình và cũng không đồng 
nghĩa với một bản sao lưu định kỳ.
1.6. Hạ tầng toàn cầu AWS
Thành phần Phạm vi và vai trò
Region Một khu vực địa lý độc lập, chứa nhiều Availability Zones. Chọn Region 
dựa trên độ trễ, tuân thủ, dịch vụ khả dụng và chi phí.
Availability Zone 
(AZ)
Một hoặc nhiều trung tâm dữ liệu tách biệt trong cùng Region, kết nối bằng 
mạng băng thông cao và độ trễ thấp. Dùng nhiều AZ để tăng tính sẵn sàng.
Edge location Điểm hiện diện gần người dùng, được các dịch vụ như CloudFront sử dụng 
để phân phối nội dung với độ trễ thấp.
1.7. Truy cập và quản lý AWS
Cách tương tác Phù hợp khi
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 5
Cách tương tác Phù hợp khi
AWS Management 
Console
Quản trị trực quan trên web, học tập và thao tác thủ công.
AWS CLI Tự động hóa bằng lệnh và tập lệnh.
AWS SDK Tích hợp API AWS vào mã nguồn ứng dụng.
API Giao tiếp theo chương trình; CLI và SDK cuối cùng đều gọi API dịch vụ.
1.8. Mô hình trách nhiệm chung
AWS - Security of the Cloud Khách hàng - Security in the Cloud
Bảo mật vật lý trung tâm dữ liệu; phần cứng; 
mạng vật lý; lớp ảo hóa; vận hành hạ tầng toàn 
cầu.
Dữ liệu; danh tính và quyền; cấu hình mạng; mã 
hóa; ứng dụng; và với EC2 là hệ điều hành 
khách cùng bản vá.
Mức trách nhiệm tăng khi dịch vụ ít được quản 
lý hơn.
Mức trách nhiệm giảm khi dùng dịch vụ 
managed, nhưng không biến mất.
1.9. AWS Well-Architected Framework
•Operational Excellence: vận hành, quan sát và cải tiến quy trình.
•Security: bảo vệ dữ liệu, hệ thống và tài sản.
•Reliability: khôi phục sau lỗi, đáp ứng nhu cầu và duy trì chức năng.
•Performance Efficiency: sử dụng tài nguyên hiệu quả theo yêu cầu.
•Cost Optimization: tránh chi phí không cần thiết và chọn mô hình chi phí phù hợp.
•Sustainability: giảm tác động môi trường của khối lượng công việc.
1.10. Các điểm dễ nhầm
Dễ nhầm Cách phân biệt
Mô hình dịch vụ và mô 
hình triển khai
IaaS/PaaS/SaaS nói về mức quản lý; public/private/hybrid/community 
nói về cách triển khai và đối tượng sử dụng.
Elasticity và scalability Scalability là khả năng đáp ứng tải lớn hơn; elasticity nhấn mạnh 
tăng/giảm tài nguyên nhanh theo nhu cầu.
Region và AZ Region là khu vực địa lý; AZ là miền lỗi tách biệt bên trong một 
Region.
CloudWatch và CloudTrail CloudWatch theo dõi hiệu năng/trạng thái; CloudTrail phục vụ audit 
hoạt động API/người dùng.
Tự kiểm tra chuyên đề 1
Sinh viên phải giải thích được 5 đặc tính cốt lõi; phân biệt IaaS/PaaS/SaaS và 4 mô hình triển 
khai; nêu vai trò hypervisor/AMI; phân biệt Region-AZ-Edge; và xác định trách nhiệm của AWS 
với khách hàng trong EC2.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 6
CHUYÊN ĐỀ 2. IDENTITY AND ACCESS MANAGEMENT (IAM)
Mục tiêu chuyên đề
Hiểu cách AWS xác thực danh tính và cấp quyền; phân biệt user, group, role, policy; áp dụng 
least privilege, MFA và temporary credentials; đọc được policy JSON đơn giản.
2.1. Xác thực và phân quyền
Khái niệm Câu hỏi cần trả lời
Authentication - Xác thực Sinh viên là ai? Dùng mật khẩu, MFA, access key hoặc temporary 
credentials để chứng minh danh tính.
Authorization - Phân quyền Sinh viên được phép làm gì trên tài nguyên nào và trong điều kiện 
nào? Được xác định bởi policies.
2.2. Các thành phần IAM
Thành phần Bản chất Cách dùng điển hình
Root user Danh tính có toàn quyền gắn với 
tài khoản AWS.
Chỉ dùng cho tác vụ bắt buộc; bật MFA; không 
tạo access key; không dùng hằng ngày.
IAM user Danh tính dài hạn cho một người 
hoặc ứng dụng trong một tài 
khoản.
Phạm vi học phần cần nắm; best practice hiện 
hành ưu tiên federation/Identity Center cho 
người dùng.
IAM group Tập hợp IAM users để gán chung 
quyền.
Gán policy cho nhóm theo vai trò công việc; 
group không dùng để đăng nhập.
IAM role Danh tính có permissions, được 
“assume” để nhận temporary 
credentials.
EC2 truy cập S3; người dùng liên tài khoản; 
cấp quyền tạm thời.
IAM policy Tài liệu JSON mô tả Effect, 
Action, Resource và điều kiện.
Gắn vào user/group/role hoặc tài nguyên tùy 
loại policy.
2.3. Cấu trúc IAM policy JSON
Ví dụ policy tối giản
{
 "Version": "2012-10-17",
 "Statement": [{
 "Effect": "Allow",
 "Action": ["s3:GetObject"],
 "Resource": "arn:aws:s3:::example-course-bucket/*"
 }]
}
Phần tử Ý nghĩa
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 7
Phần tử Ý nghĩa
Version Phiên bản ngôn ngữ policy.
Statement Một hoặc nhiều phát biểu quyền.
Effect Allow hoặc Deny.
Action Thao tác API được cho phép/từ chối, ví dụ ec2:RunInstances.
Resource Tài nguyên áp dụng, thường biểu diễn bằng ARN.
Condition Điều kiện bổ sung như IP nguồn, thời gian, MFA hoặc tag.
Principal Danh tính được áp dụng trong resource-based policy hoặc trust policy.
2.4. Logic đánh giá quyền
1. Mặc định là implicit deny. Nếu không có policy nào cho phép, yêu cầu bị từ chối.
2. Cần explicit allow. Một policy phù hợp phải cho phép Action trên Resource trong đúng điều 
kiện.
3. Explicit deny luôn thắng. Nếu có bất kỳ Deny phù hợp nào, yêu cầu bị từ chối dù một policy 
khác có Allow.
Công thức ghi nhớ
Default Deny → tìm Allow → kiểm tra Deny. Một Explicit Deny có thể phủ định mọi Allow liên 
quan.
2.5. Quyền cho ứng dụng chạy trên EC2
Khi một ứng dụng trên EC2 cần truy cập S3, DynamoDB hoặc dịch vụ AWS khác, cách an toàn là:
1. Tạo policy chỉ cho phép đúng thao tác và tài nguyên cần thiết.
2. Gắn policy vào một IAM role.
3. Gắn role đó vào EC2 instance thông qua instance profile.
4. AWS cung cấp temporary credentials tự động; không lưu access key cố định trong mã nguồn 
hoặc AMI.
2.6. Best practices cần ghi nhớ
•Bật MFA cho root user và các danh tính cần bảo vệ.
•Không dùng root user cho công việc hằng ngày.
•Áp dụng least privilege: chỉ cấp quyền tối thiểu cần thiết.
•Ưu tiên IAM roles và temporary credentials cho workload.
•Không nhúng access keys vào mã nguồn, ảnh máy ảo hoặc kho Git.
•Xóa/vô hiệu hóa users, roles, policies và credentials không còn dùng.
•Dùng CloudTrail để audit ai đã gọi API nào, vào thời điểm nào và trên tài nguyên nào.
2.7. IAM, CloudTrail và mô hình trách nhiệm chung
Tình huống Dịch vụ/Trách nhiệm phù hợp
Tạo danh tính và cấp quyền truy cập AWS IAM.
Kiểm tra ai đã xóa hoặc dừng một EC2 instance CloudTrail.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 8
Tình huống Dịch vụ/Trách nhiệm phù hợp
Bảo mật vật lý, hypervisor và phân tách hạ tầng AWS.
MFA, access keys, policies, Security Groups và 
dữ liệu
Khách hàng.
Vá hệ điều hành khách trên EC2 Khách hàng.
Vá engine/hệ điều hành nền của dịch vụ 
database managed
AWS; khách hàng vẫn quản lý dữ liệu, tài khoản 
DB và cấu hình phù hợp.
2.8. Các điểm dễ nhầm
Dễ nhầm Cách phân biệt
Group và role Group chỉ gom users; role được assume và cung cấp temporary 
credentials.
IAM và CloudTrail IAM quyết định quyền; CloudTrail ghi lại hoạt động API để audit.
MFA và authorization MFA tăng độ tin cậy của xác thực; quyền cụ thể vẫn do policies quyết 
định.
Console password và 
access keys
Mật khẩu dùng đăng nhập Console; access key/temporary credentials 
dùng truy cập theo chương trình.
Tự kiểm tra chuyên đề 2
Sinh viên phải chọn được đúng IAM entity cho từng tình huống; giải thích policy JSON; áp dụng 
logic Deny/Allow; nêu quy trình EC2 dùng role để truy cập S3; và phân biệt IAM với CloudTrail.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 9
CHUYÊN ĐỀ 3. NETWORK
Mục tiêu: Đọc được cấu trúc mạng AWS cơ bản; tính địa chỉ CIDR; phân biệt public/private 
subnet, Security Group/Network ACL; chọn Internet Gateway, NAT Gateway, VPN, Direct 
Connect và edge location theo tình huống.
3.1. Phạm vi của VPC và subnet
Đối tượng Phạm vi
VPC Thuộc một AWS Region và có thể chứa subnet ở nhiều Availability Zones trong 
Region đó.
Subnet Thuộc đúng một Availability Zone; là một dải địa chỉ IP con của VPC.
EC2 network 
interface (ENI)
Đặt trong một subnet và nhận private IP; có thể gắn Security Groups.
3.2. CIDR và số địa chỉ IP khả dụng
Với IPv4, số địa chỉ của một khối /n là 2^(32-n). Trong mỗi subnet, AWS dành riêng 5 địa chỉ IPv4; 
do đó:
Công thức
Số IPv4 có thể gán cho tài nguyên = 2^(32 - prefix) - 5
CIDR Tổng địa chỉ Địa chỉ có thể gán trong subnet AWS
/24 256 251
/26 64 59
/27 32 27
/28 16 11
Ghi nhớ phạm vi thường gặp: VPC/subnet IPv4 được tạo với prefix từ /16 đến /28. Các subnet 
trong cùng VPC không được chồng lấn CIDR.
3.3. Public subnet và private subnet
Public subnet Private subnet
Route table có route đến Internet Gateway 
(IGW). Tài nguyên còn cần public IPv4/EIP và 
Security Group/NACL phù hợp để truy cập trực 
tiếp từ Internet.
Không có route trực tiếp đến IGW. Tài nguyên 
thường chỉ dùng private IP.
Phù hợp cho ALB internet-facing, NAT 
Gateway, bastion hoặc web server cần public 
access.
Phù hợp cho application/database servers không 
cần nhận kết nối trực tiếp từ Internet.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 10
Public subnet Private subnet
Có thể giao tiếp Internet hai chiều nếu cấu hình 
đầy đủ.
Muốn cập nhật phần mềm ra Internet thường đi 
qua NAT Gateway đặt trong public subnet. NAT 
không cho phép kết nối Internet khởi tạo trực 
tiếp vào tài nguyên private.
3.4. Route table, Internet Gateway và NAT Gateway
Thành phần Vai trò
Route table Quyết định đích đến và target của lưu lượng từ subnet. Local route cho phép 
các subnet trong VPC giao tiếp và không thể xóa.
Internet Gateway Gắn vào VPC để hỗ trợ kết nối giữa tài nguyên có public IP và Internet.
NAT Gateway Cho phép tài nguyên trong private subnet khởi tạo kết nối ra Internet; đặt 
trong public subnet và cần route ra IGW.
Elastic IP Địa chỉ IPv4 công cộng tĩnh có thể gán/remap cho tài nguyên tương thích; 
có thể phát sinh chi phí.
3.5. Security Group và Network ACL
Tiêu chí Security Group Network ACL
Phạm vi Gắn với ENI/tài nguyên. Áp dụng ở mức subnet.
Trạng thái Stateful: lưu lượng phản hồi tự động 
được cho phép.
Stateless: phải cấu hình cả inbound và 
outbound.
Rule Chỉ có allow rules. Có allow và deny rules; đánh giá theo 
thứ tự số rule.
Mức sử dụng Lớp bảo vệ chính cho EC2/ENI. Lớp kiểm soát bổ sung ở ranh giới 
subnet.
Nhận diện nhanh
“Gắn với instance/ENI, stateful” → Security Group. “Ở mức subnet, stateless, có allow/deny” → 
Network ACL.
3.6. Kết nối với hệ thống tại chỗ
Giải pháp Đặc điểm
AWS Site-to-Site VPN Kết nối mã hóa qua Internet; triển khai nhanh; hiệu năng phụ thuộc 
đường Internet.
AWS Direct Connect Kết nối mạng chuyên dụng từ on-premises đến AWS; ổn định hơn cho 
lưu lượng lớn và yêu cầu nhất quán.
Kết hợp VPN + Direct 
Connect
Có thể dùng VPN để tăng bảo mật hoặc làm phương án dự phòng tùy 
kiến trúc.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 11
3.7. Tính sẵn sàng và độ trễ
•Triển khai trên ít nhất hai Availability Zones để tránh một miền lỗi duy nhất.
•Multi-Region phù hợp khi cần phục vụ người dùng ở khu vực địa lý khác, đáp ứng yêu cầu DR 
hoặc giảm độ trễ toàn cầu.
•CloudFront dùng edge locations để cache nội dung gần người dùng.
•Các AZ trong cùng Region kết nối độ trễ thấp, hỗ trợ kiến trúc đồng bộ và dự phòng.
3.8. Sơ đồ logic cần hình dung
Luồng Internet vào ứng dụng Luồng từ private subnet ra Internet
Internet → IGW → route table public subnet → 
ALB/EC2 có public path → Security Group.
Private EC2 → route table private subnet → 
NAT Gateway trong public subnet → IGW → 
Internet.
Không phải mọi tài nguyên trong public subnet 
đều tự động public; còn phụ thuộc public IP và 
rule bảo mật.
NAT Gateway không biến private EC2 thành 
máy chủ có thể nhận kết nối trực tiếp từ Internet.
3.9. Các điểm dễ nhầm
Dễ nhầm Cách phân biệt
Public subnet và public IP Public subnet được xác định bởi route đến IGW; EC2 vẫn cần public 
IP/EIP để giao tiếp Internet trực tiếp.
IGW và NAT Gateway IGW hỗ trợ kết nối Internet của VPC; NAT Gateway chủ yếu cho 
private subnet đi ra ngoài.
Security Group và firewall 
truyền thống
SG stateful và chỉ allow; không có explicit deny.
High availability và low 
latency
Nhiều AZ tăng availability; triển khai Region gần người dùng/edge 
giảm latency.
Tự kiểm tra chuyên đề 3
Sinh viên phải tính đúng số IP khả dụng; xác định phạm vi Region/VPC/AZ/subnet; vẽ được 
luồng IGW và NAT; phân biệt SG-NACL; và chọn VPN/Direct Connect/CloudFront theo yêu 
cầu.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 12
CHUYÊN ĐỀ 4. COMPUTE, STORAGE, DATABASE
Mục tiêu: Chọn đúng dịch vụ compute, storage và database theo loại workload; hiểu 
EC2/AMI/lifecycle/pricing; phân biệt S3, EBS, EFS, Instance Store; phân biệt RDS/Aurora và 
DynamoDB.
4.1. Amazon EC2
Thành phần khi khởi 
chạy Ý nghĩa
AMI Hệ điều hành và nội dung mẫu để tạo instance.
Instance type Cấu hình CPU, RAM, mạng và đặc tính phần cứng.
Network VPC, subnet, địa chỉ IP và Security Groups; có thể dùng giá trị mặc định 
hoặc cấu hình rõ ràng.
Storage EBS volumes hoặc instance store tùy loại instance.
Key pair / cơ chế truy 
cập
SSH cho Linux; RDP cho Windows. Mật khẩu Administrator của 
Windows có thể được giải mã bằng private key tương ứng.
User data Tập lệnh khởi tạo để cài đặt/cấu hình tự động khi instance khởi chạy.
4.2. Vòng đời EC2 và chi phí
Trạng thái Điều cần nhớ
Pending → Running Instance được cấp phát và bắt đầu hoạt động.
Rebooting Khởi động lại hệ điều hành; thường giữ nguyên host và địa chỉ mạng.
Stopped Compute charge của instance dừng, nhưng EBS volumes, snapshots, public 
IPv4 hoặc tài nguyên liên quan vẫn có thể phát sinh chi phí. Khi start lại có 
thể chạy trên host vật lý khác.
Terminated Instance bị xóa; hành vi EBS root volume phụ thuộc DeleteOnTermination. 
Instance store bị mất.
Cảnh báo dễ nhầm
Không được suy luận “Stopped = không còn mọi chi phí”. Chỉ chi phí compute của EC2 instance 
dừng; các tài nguyên lưu trữ và mạng liên quan có thể tiếp tục tính phí.
4.3. Lựa chọn mô hình chi phí EC2
Tùy chọn Phù hợp với
On-Demand Nhu cầu ngắn hạn, không dự đoán được, không muốn cam kết.
Savings Plans / Reserved 
Instances
Khối lượng ổn định, dự đoán được và có thể cam kết để giảm chi phí. 
Reserved Instance chủ yếu là lợi ích giá, không phải một máy vật lý 
riêng.
Spot Instances Batch, xử lý song song, CI/CD hoặc workload chịu được gián đoạn.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 13
Tùy chọn Phù hợp với
Dedicated Hosts Yêu cầu phần cứng vật lý dành riêng, licensing hoặc tuân thủ.
Capacity Reservations Cần đảm bảo công suất On-Demand trong một AZ.
4.4. EC2, Lambda và Elastic Beanstalk
Dịch vụ Mô hình Khi nên chọn
Amazon EC2 IaaS Cần kiểm soát hệ điều hành, runtime, mạng và phần mềm.
AWS Lambda Serverless 
compute
Mã chạy theo sự kiện, thời lượng ngắn, tự động mở rộng, 
không quản lý máy chủ.
AWS Elastic Beanstalk PaaS Muốn triển khai web app nhanh; AWS cung cấp EC2, load 
balancing, monitoring và scaling phía dưới.
4.5. So sánh các loại lưu trữ
Dịch vụ Loại Phạm vi và đặc điểm Tình huống
Amazon S3 Object Dung lượng mở rộng rất lớn; truy cập 
qua API; độ bền cao; không gắn như 
ổ đĩa hệ điều hành thông thường.
Ảnh/video, backup, data 
lake, static website, nguồn 
cho CloudFront.
Amazon EBS Block Volume gắn với EC2; nằm trong một 
AZ; phù hợp ổ hệ điều hành và 
database. Snapshot là incremental.
Boot volume, database, ứng 
dụng cần block storage.
Amazon EFS File/NFS Hệ thống file dùng chung, có thể 
mount đồng thời từ nhiều EC2; mở 
rộng tự động.
Shared web content, home 
directory, workload Linux 
dùng NFS.
Instance Store Ephemeral 
block
Lưu trữ tạm trên host; dữ liệu mất khi 
instance stop/terminate hoặc host lỗi.
Cache, scratch data, dữ liệu 
có thể tái tạo.
4.6. Database
Dịch vụ Loại Đặc điểm chính
Amazon RDS Relational managed 
database
Hỗ trợ nhiều engine; AWS quản lý hạ tầng, backup 
và patching theo dịch vụ; khách hàng quản lý 
schema, dữ liệu, tài khoản DB và cấu hình.
Amazon Aurora Relational, tương thích 
MySQL/PostgreSQL
Hiệu năng và tính sẵn sàng cao; phù hợp ứng dụng 
quan hệ quan trọng.
Amazon 
DynamoDB
NoSQL keyvalue/document
Serverless, độ trễ thấp, tự động mở rộng; phù hợp 
truy cập theo khóa ở quy mô lớn.
AWS Database 
Migration Service
Migration Di chuyển/đồng bộ dữ liệu giữa nguồn và đích với 
thời gian gián đoạn thấp tùy cấu hình.
4.7. Multi-AZ, high availability và fault tolerance
•RDS Multi-AZ duy trì bản sao dự phòng ở AZ khác và hỗ trợ failover tự động; mục tiêu chính là 
availability, không phải mở rộng đọc.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 14
•S3 và DynamoDB được thiết kế theo kiến trúc managed phân tán; người dùng không tự gắn một 
volume vào nhiều AZ.
•EC2 high availability thường cần nhiều instances ở nhiều AZ, đi cùng ELB và Auto Scaling.
4.8. Ma trận chọn nhanh
Yêu cầu Lựa chọn ưu tiên
Lưu ảnh/video hoặc static content Amazon S3.
Ổ đĩa hệ điều hành/database cho một EC2 Amazon EBS.
NFS dùng chung cho nhiều EC2 Amazon EFS.
Dữ liệu tạm, cache, scratch EC2 Instance Store.
Cơ sở dữ liệu quan hệ managed Amazon RDS hoặc Aurora.
NoSQL key-value, độ trễ thấp, scale lớn Amazon DynamoDB.
Chạy mã khi có event, không quản lý server AWS Lambda.
Triển khai web app mà không muốn quản lý hạ 
tầng chi tiết
Elastic Beanstalk.
4.9. Các điểm dễ nhầm
Dễ nhầm Cách phân biệt
S3 và EBS S3 là object storage qua API; EBS là block volume gắn với EC2.
EBS và EFS EBS thường cho một instance trong một AZ; EFS là file system dùng 
chung cho nhiều instances.
RDS và DynamoDB RDS quan hệ/SQL; DynamoDB NoSQL key-value/document.
AMI và EBS snapshot AMI là mẫu khởi chạy instance; EBS snapshot là bản sao incremental 
của volume.
High availability và backup Multi-AZ/failover duy trì dịch vụ; snapshot/backup phục hồi dữ liệu. 
Hai mục tiêu khác nhau.
Tự kiểm tra chuyên đề 4
Sinh viên phải chọn được đúng compute/storage/database theo workload; giải thích vòng đời và 
chi phí EC2; phân biệt AMI-snapshot; hiểu Spot/Dedicated/On-Demand; và nêu trách nhiệm của 
khách hàng khi dùng EC2 so với RDS/DynamoDB.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 15
CHUYÊN ĐỀ 5. ELB, SCALING, MONITOR
Mục tiêu: Hiểu mối quan hệ giữa load balancing, scaling, high availability và monitoring; chọn 
đúng ALB/NLB/GWLB/CLB; cấu hình tư duy Auto Scaling; phân biệt CloudWatch và 
CloudTrail.
5.1. Scalability, elasticity, high availability, fault tolerance
Khái niệm Ý nghĩa
Vertical scaling Tăng cấu hình của một máy: thêm CPU/RAM; thường có giới hạn và 
có thể cần gián đoạn.
Horizontal scaling Thêm/bớt nhiều instances hoặc nodes.
Elasticity Tự động tăng và giảm tài nguyên theo nhu cầu thực tế.
High availability Giảm thời gian gián đoạn bằng dự phòng và phân tán qua nhiều miền 
lỗi.
Fault tolerance Hệ thống tiếp tục hoạt động khi một thành phần bị lỗi, thường với 
mức dự phòng cao hơn.
5.2. Elastic Load Balancing
ELB phân phối lưu lượng đến các targets khỏe mạnh, thực hiện health checks và giúp loại bỏ một 
điểm truy cập đơn lẻ. ELB không thay thế Auto Scaling: ELB phân phối lưu lượng; Auto Scaling 
tạo, xóa hoặc thay thế compute capacity.
Loại Lớp/Giao thức Tình huống chính
Application Load Balancer 
(ALB)
Layer 7: HTTP/HTTPS Host/path/header routing, microservices, 
containers, Lambda targets, web 
application.
Network Load Balancer 
(NLB)
Layer 4: 
TCP/UDP/TLS
Thông lượng rất cao, độ trễ thấp, lưu lượng 
đột biến, static IP/EIP, IP targets.
Gateway Load Balancer 
(GWLB)
Layer 3/4 appliance 
traffic
Triển khai và mở rộng thiết bị mạng ảo như 
firewall/IDS/IPS.
Classic Load Balancer 
(CLB)
Thế hệ trước Workload legacy; với hệ thống mới thường 
ưu tiên ALB hoặc NLB.
5.3. Auto Scaling Group
Thành phần Ý nghĩa
Minimum capacity Số instance tối thiểu luôn được duy trì.
Desired capacity Số instance ASG cố gắng duy trì tại thời điểm hiện tại.
Maximum capacity Giới hạn trên của số instance.
Launch template AMI, instance type, Security Group, storage và cấu hình khởi chạy.
Health checks Phát hiện instance lỗi và thay thế; có thể kết hợp EC2 status và ELB 
health checks.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 16
Thành phần Ý nghĩa
Multi-AZ Phân bố instances qua nhiều AZ để tăng availability.
5.4. Scaling policies
Policy Cách hoạt động
Target tracking Duy trì metric quanh một giá trị mục tiêu, ví dụ CPU trung bình 
khoảng 50%. AWS quản lý CloudWatch alarms liên quan.
Step scaling Tăng/giảm theo các ngưỡng và bước khác nhau.
Scheduled scaling Thay đổi capacity theo lịch biết trước, ví dụ trước giờ mở bán.
Predictive scaling Dự báo pattern tải và chuẩn bị capacity trước.
5.5. Amazon CloudWatch
Thành phần Mục đích
Metrics Số liệu theo thời gian như CPUUtilization, request count, latency.
Logs Thu thập và phân tích log hệ thống/ứng dụng.
Alarms Theo dõi metric và chuyển trạng thái khi vượt ngưỡng; có thể gửi 
thông báo hoặc kích hoạt hành động.
Dashboards Trực quan hóa metrics và alarms.
Events/EventBridge 
integration
Phản ứng theo sự kiện vận hành và thay đổi trạng thái.
5.6. CloudWatch và CloudTrail
Câu hỏi CloudWatch CloudTrail
Theo dõi điều gì? Hiệu năng, logs, metrics, trạng thái 
vận hành.
Hoạt động người dùng, role và API.
Ví dụ CPU > 70%, latency tăng, log ứng 
dụng có lỗi.
Ai đã terminate instance? Ai thay đổi 
Security Group?
Mục tiêu chính Monitoring, observability và alarm. Audit, governance, security 
investigation.
5.7. Kiến trúc web có tính sẵn sàng cao
Lớp Thiết kế điển hình
DNS/CDN Route 53/CloudFront tùy yêu cầu toàn cầu.
Load balancing ALB đặt trước các web/app instances.
Compute EC2 Auto Scaling Group trải trên ít nhất hai AZ.
Database RDS Multi-AZ hoặc dịch vụ database managed phù hợp.
Monitoring CloudWatch metrics/logs/alarms; CloudTrail audit thay đổi.
Decoupling SQS giúp các thành phần trao đổi bất đồng bộ và giảm phụ thuộc trực tiếp.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 17
5.8. Các điểm dễ nhầm
Dễ nhầm Cách phân biệt
ELB và Auto Scaling ELB phân phối request; Auto Scaling thay đổi số lượng/công suất 
compute.
ALB và NLB ALB hiểu HTTP layer 7; NLB xử lý TCP/UDP/TLS layer 4 với hiệu 
năng cao và IP tĩnh.
CloudWatch Alarm và Auto 
Scaling
Alarm quan sát metric; scaling policy quyết định hành động thay đổi 
capacity. Target tracking có thể tự tạo/quản lý alarms.
High availability và elasticity HA chống lỗi; elasticity xử lý biến động tải. Một kiến trúc tốt 
thường cần cả hai.
Tự kiểm tra chuyên đề 5
Sinh viên phải chọn được ALB/NLB/GWLB/CLB; giải thích min/desired/max; phân biệt target 
tracking, step và scheduled scaling; nhận diện CloudWatch so với CloudTrail; và mô tả kiến trúc 
ALB + ASG + Multi-AZ.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 18
BẢNG TỔNG HỢP NHẬN DIỆN NHANH
Từ khóa trong tình huống Khái niệm/Dịch vụ nên nghĩ tới
Tự cấp phát, trả theo sử dụng, mở rộng nhanh Đặc tính điện toán đám mây.
Chỉ tập trung viết và triển khai ứng dụng PaaS / Elastic Beanstalk.
Toàn quyền hệ điều hành máy chủ ảo IaaS / Amazon EC2.
Dùng ứng dụng hoàn chỉnh qua Internet SaaS.
Kết hợp on-premises và public cloud Hybrid cloud.
Cấp quyền tạm thời cho EC2 truy cập S3 IAM role.
Mặc định từ chối; Deny thắng Allow IAM policy evaluation.
Ai đã gọi API/xóa tài nguyên? AWS CloudTrail.
CPU, logs, latency, alarm Amazon CloudWatch.
Mạng riêng logic trong một Region Amazon VPC.
Subnet ra Internet trực tiếp Route đến IGW + public IP + rule bảo mật.
Private subnet tải bản cập nhật từ Internet NAT Gateway trong public subnet.
Stateful, gắn với ENI/instance Security Group.
Stateless, subnet, allow/deny Network ACL.
Object storage cho ảnh/video/static website Amazon S3.
Block storage cho EC2/database Amazon EBS.
Shared NFS cho nhiều EC2 Amazon EFS.
Dữ liệu tạm trên host Instance Store.
Relational managed database Amazon RDS / Aurora.
NoSQL key-value, độ trễ thấp Amazon DynamoDB.
Event-driven, không quản lý server AWS Lambda.
HTTP/HTTPS, path/host routing Application Load Balancer.
TCP/UDP, thông lượng cao, static IP Network Load Balancer.
Thêm/bớt EC2 theo metric EC2 Auto Scaling.
Phân tán qua nhiều AZ High availability / Reliability.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 19
CÂU HỎI TỰ LUYỆN ĐỘC LẬP
Cách làm
Làm toàn bộ câu hỏi mà không xem đáp án. Với mỗi câu sai, ghi lại từ khóa quyết định, quy tắc 
liên quan và lý do loại từng phương án. Các câu dưới đây được biên soạn mới, không phải câu hỏi 
trích từ đề thi.
A. Overview
Câu 1. Một nhóm phát triển muốn đưa ứng dụng web lên cloud nhưng không muốn quản lý hệ điều 
hành, runtime và cấu hình máy chủ. Mô hình dịch vụ phù hợp nhất là gì?
A. IaaS
B. PaaS
C. SaaS
D. Private cloud
Câu 2. Đặc tính nào của cloud thể hiện việc mức sử dụng tài nguyên được đo đếm và làm cơ sở tính 
phí?
A. Resource pooling
B. Broad network access
C. Measured service
D. Community cloud
Câu 3. Doanh nghiệp giữ hệ thống dữ liệu nhạy cảm tại trung tâm dữ liệu riêng nhưng sử dụng 
public cloud khi nhu cầu tăng cao. Đây là mô hình nào?
A. Public cloud
B. Private cloud
C. Hybrid cloud
D. SaaS
Câu 4. Trong mô hình trách nhiệm chung khi sử dụng Amazon EC2, nội dung nào thuộc trách nhiệm 
của AWS?
A. Vá ứng dụng do khách hàng cài đặt
B. Cấu hình Security Group
C. Bảo mật phần cứng và lớp ảo hóa
D. Quản lý tài khoản người dùng trong ứng dụng
Câu 5. Phát biểu nào đúng về Availability Zone?
A. Là một khu vực địa lý chứa nhiều Regions
B. Là miền lỗi tách biệt nằm trong một Region
C. Là điểm cache nội dung của CloudFront
D. Là mạng ảo riêng của một tài khoản
Câu 6. Thành phần nào đóng vai trò quản lý và phân phối tài nguyên phần cứng cho các máy ảo?
A. IAM policy
B. Hypervisor
C. Route table
D. Load balancer
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 20
Câu 7. Một ứng dụng hoàn chỉnh được cung cấp cho người dùng qua trình duyệt, người dùng không 
quản lý hạ tầng hay runtime. Đây là mô hình nào?
A. SaaS
B. PaaS
C. IaaS
D. Hybrid cloud
Câu 8. Trụ cột nào của AWS Well-Architected tập trung vào khả năng khôi phục sau lỗi và duy trì 
chức năng?
A. Cost Optimization
B. Reliability
C. Sustainability
D. Performance Efficiency
B. IAM
Câu 9. Một ứng dụng trên EC2 cần đọc dữ liệu từ một S3 bucket. Phương án bảo mật tốt nhất là gì?
A. Lưu access key của root user trong mã nguồn
B. Gắn IAM role có quyền tối thiểu vào EC2
C. Công khai S3 bucket
D. Dùng chung mật khẩu Console của quản trị viên
Câu 10. Một identity có policy Allow s3:GetObject nhưng một policy khác có explicit Deny cho 
cùng hành động và tài nguyên. Kết quả là gì?
A. Allow vì policy đầu tiên được đọc trước
B. Allow nếu user bật MFA
C. Deny vì explicit Deny ưu tiên
D. Phụ thuộc Region
Câu 11. Đâu là cách dùng root user phù hợp nhất?
A. Dùng cho mọi công việc quản trị hằng ngày
B. Tạo access keys và chia sẻ cho nhóm
C. Chỉ dùng cho tác vụ bắt buộc, bảo vệ bằng MFA
D. Dùng thay thế IAM role cho EC2
Câu 12. Thành phần IAM nào gom nhiều IAM users để gán chung permissions?
A. IAM group
B. IAM role
C. Resource policy
D. Access key
Câu 13. Trong IAM policy, phần tử nào mô tả thao tác API như ec2:StartInstances?
A. Effect
B. Action
C. Version
D. Principal
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 21
Câu 14. Dịch vụ nào phù hợp để xác định danh tính đã thay đổi một Security Group?
A. CloudWatch Metrics
B. CloudTrail
C. Auto Scaling
D. Elastic Load Balancing
Câu 15. MFA giúp tăng cường khía cạnh nào?
A. Mã hóa dữ liệu lưu trữ
B. Xác thực danh tính
C. Tự động mở rộng tài nguyên
D. Định tuyến mạng
Câu 16. Những thực hành nào phù hợp với least privilege? (Chọn nhiều đáp án.)
A. Cấp AdministratorAccess cho mọi user
B. Chỉ cho phép đúng actions và resources cần thiết
C. Dùng wildcard * trong mọi policy
D. Xóa quyền không còn sử dụng
C. Network
Câu 17. Điều kiện quan trọng để một subnet được coi là public là gì?
A. Có tên chứa từ public
B. Route table có route tới Internet Gateway
C. Mọi EC2 có private IP
D. Có Network ACL mặc định
Câu 18. Một EC2 trong private subnet cần truy cập Internet để cập nhật phần mềm nhưng không 
được nhận kết nối khởi tạo từ Internet. Giải pháp phù hợp là gì?
A. Gắn Internet Gateway trực tiếp vào EC2
B. Dùng NAT Gateway trong public subnet
C. Gán public IP và mở tất cả cổng
D. Chỉ thêm Security Group outbound
Câu 19. Cơ chế nào stateful và áp dụng ở mức ENI/instance?
A. Network ACL
B. Security Group
C. Route table
D. Internet Gateway
Câu 20. Cơ chế nào stateless, có cả allow và deny rules và áp dụng ở mức subnet?
A. Security Group
B. IAM policy
C. Network ACL
D. CloudTrail
Câu 21. Một subnet IPv4 /27 trong AWS có bao nhiêu địa chỉ có thể gán cho tài nguyên?
A. 32
B. 30
C. 27
D. 25
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 22
Câu 22. Phát biểu nào đúng?
A. VPC thuộc một AZ duy nhất
B. Subnet có thể trải trên nhiều AZ
C. VPC thuộc một Region; subnet thuộc một AZ
D. Region nằm trong VPC
Câu 23. Doanh nghiệp cần kết nối mạng chuyên dụng ổn định từ data center tại chỗ tới AWS cho lưu 
lượng lớn. Dịch vụ phù hợp nhất là gì?
A. AWS Direct Connect
B. Amazon CloudFront
C. Internet Gateway
D. Elastic IP
Câu 24. Dịch vụ nào tận dụng edge locations để giảm độ trễ phân phối nội dung?
A. Amazon RDS
B. Amazon CloudFront
C. Amazon EBS
D. AWS IAM
D. Compute, Storage, Database
Câu 25. Ứng dụng cần lưu hàng triệu ảnh và video với khả năng mở rộng gần như không giới hạn. 
Dịch vụ phù hợp nhất là gì?
A. Amazon EBS
B. Amazon S3
C. Instance Store
D. Amazon SQS
Câu 26. Nhiều EC2 Linux ở các AZ khác nhau cần dùng chung một hệ thống file NFS. Nên chọn gì?
A. Amazon EFS
B. Amazon EBS
C. Instance Store
D. Amazon DynamoDB
Câu 27. Một database chạy trên EC2 cần block storage bền vững và có thể snapshot. Nên chọn gì?
A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. CloudFront
Câu 28. Dữ liệu scratch có thể tái tạo, cần tốc độ cao và không cần giữ khi instance dừng. Nên dùng 
gì?
A. EBS gp volume
B. S3 Standard
C. Instance Store
D. RDS Multi-AZ
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 23
Câu 29. Một batch job có thể bị gián đoạn và chạy lại, mục tiêu chính là giảm chi phí compute. Lựa 
chọn phù hợp nhất là gì?
A. Dedicated Hosts
B. Spot Instances
C. On-Demand Capacity Reservation
D. RDS Reserved DB
Câu 30. Mã xử lý chỉ chạy khi có file mới được tải lên S3 và không muốn quản lý máy chủ. Nên 
dùng gì?
A. Amazon EC2
B. AWS Lambda
C. Amazon EFS
D. AWS Direct Connect
Câu 31. Ứng dụng cần cơ sở dữ liệu quan hệ managed và failover tự động giữa các AZ. Lựa chọn 
phù hợp là gì?
A. DynamoDB global table
B. RDS Multi-AZ
C. S3 Versioning
D. EC2 Instance Store
Câu 32. AMI chủ yếu được dùng để làm gì?
A. Theo dõi metric của EC2
B. Làm mẫu khởi chạy EC2 instances
C. Cân bằng tải HTTP
D. Cấp quyền IAM
E. ELB, Scaling, Monitor
Câu 33. Ứng dụng HTTP cần định tuyến /api và /images tới các target groups khác nhau. Nên dùng 
loại load balancer nào?
A. Network Load Balancer
B. Application Load Balancer
C. Gateway Load Balancer
D. Classic Load Balancer bắt buộc
Câu 34. Dịch vụ cần xử lý TCP với lưu lượng tăng đột biến, độ trễ thấp và yêu cầu địa chỉ IP tĩnh. 
Nên dùng gì?
A. Application Load Balancer
B. Network Load Balancer
C. Amazon CloudWatch
D. AWS Lambda
Câu 35. Trong Auto Scaling Group, tham số nào thể hiện số instance mà nhóm cố gắng duy trì hiện 
tại?
A. Minimum capacity
B. Desired capacity
C. Maximum capacity
D. Cooldown
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 24
Câu 36. Dịch vụ nào thu thập metrics, logs và tạo alarms?
A. AWS CloudTrail
B. Amazon CloudWatch
C. AWS IAM
D. AWS Artifact
Câu 37. Chính sách scaling nào phù hợp để duy trì CPU trung bình quanh 50%?
A. Target tracking
B. Manual scaling
C. Network ACL
D. Reserved scaling
Câu 38. Thiết kế nào tăng tính sẵn sàng cho web application?
A. Một EC2 lớn trong một AZ
B. ALB và Auto Scaling Group trải trên nhiều AZ
C. Chỉ dùng EBS snapshot
D. Gán nhiều Security Groups cho một EC2
Câu 39. Khi target không vượt qua health check, ELB thường làm gì?
A. Tiếp tục gửi toàn bộ traffic để kiểm tra
B. Ngừng định tuyến traffic tới target đó cho đến khi khỏe lại
C. Tự đổi IAM role của target
D. Tự chuyển database sang NoSQL
Câu 40. Phát biểu nào đúng về ELB và Auto Scaling?
A. ELB tự tạo thêm EC2 nên không cần Auto Scaling
B. Auto Scaling phân phối HTTP request theo path
C. ELB phân phối traffic; Auto Scaling điều chỉnh compute capacity
D. Hai dịch vụ chỉ dùng được trong một AZ
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 25
ĐÁP ÁN VÀ GIẢI THÍCH NGẮN
Câu Đáp án Giải thích
1 B PaaS cho phép nhóm tập trung vào mã và dữ liệu, trong khi nền tảng quản lý hệ 
điều hành/runtime.
2 C Measured service là khả năng đo đếm mức sử dụng để giám sát và tính phí.
3 C Hybrid cloud kết hợp hạ tầng riêng/on-premises với public cloud.
4 C AWS chịu trách nhiệm về phần cứng, cơ sở vật lý và lớp ảo hóa.
5 B AZ là miền lỗi tách biệt trong một Region.
6 B Hypervisor/VMM quản lý tài nguyên cho các máy ảo.
7 A SaaS cung cấp ứng dụng hoàn chỉnh cho người dùng.
8 B Reliability tập trung vào hoạt động ổn định và khôi phục sau lỗi.
9 B IAM role cung cấp temporary credentials cho EC2, tránh khóa dài hạn.
10 C Explicit Deny luôn ghi đè Allow phù hợp.
11 C Root user chỉ nên dùng cho tác vụ bắt buộc và phải bật MFA.
12 A IAM group là tập hợp IAM users để gán quyền chung.
13 B Action mô tả thao tác API được phép hoặc bị từ chối.
14 B CloudTrail ghi nhận hoạt động API và danh tính thực hiện.
15 B MFA bổ sung một yếu tố để xác thực danh tính.
16 B, D Least privilege yêu cầu cấp đúng quyền cần thiết và loại bỏ quyền dư thừa.
17 B Route table có route tới IGW là tiêu chí mạng của public subnet.
18 B NAT Gateway cho phép private resources khởi tạo kết nối ra Internet.
19 B Security Group stateful và gắn với ENI/tài nguyên.
20 C Network ACL stateless, áp dụng subnet và có allow/deny.
21 C /27 có 32 địa chỉ; AWS dành 5 nên còn 27 địa chỉ có thể gán.
22 C VPC là tài nguyên theo Region; mỗi subnet thuộc một AZ.
23 A Direct Connect cung cấp kết nối chuyên dụng từ on-premises tới AWS.
24 B CloudFront phân phối nội dung qua edge locations.
25 B S3 phù hợp object storage cho ảnh/video ở quy mô lớn.
26 A EFS là file system NFS dùng chung cho nhiều EC2.
27 B EBS là block storage bền vững cho EC2 và hỗ trợ snapshots.
28 C Instance Store là lưu trữ tạm, dữ liệu có thể mất khi stop/terminate.
29 B Spot phù hợp workload chịu được gián đoạn và ưu tiên chi phí.
30 B Lambda chạy mã theo sự kiện mà không quản lý server.
31 B RDS Multi-AZ cung cấp database quan hệ managed với failover.
TÀI LIỆU ÔN TẬP HỌC PHẦN ĐIỆN TOÁN ĐÁM MÂY
Trang 26
Câu Đáp án Giải thích
32 B AMI là mẫu để tạo EC2 instance có cấu hình nhất quán.
33 B ALB hỗ trợ định tuyến HTTP theo path/host.
34 B NLB phù hợp TCP/UDP, throughput cao, latency thấp và IP tĩnh.
35 B Desired capacity là số instance ASG cố gắng duy trì hiện tại.
36 B CloudWatch thu metrics/logs và tạo alarms.
37 A Target tracking tự điều chỉnh capacity để metric gần giá trị mục tiêu.
38 B ALB + ASG multi-AZ loại bỏ single point of failure ở compute layer.
39 B ELB ngừng gửi traffic đến target unhealthy và đưa lại khi health check đạt.
40 C ELB và Auto Scaling bổ trợ nhau nhưng có chức năng khác nhau.
TÀI LIỆU THAM KHẢO
[1] Slides Tổng quan và tài liệu học tập của học phần. 
[2] Coursera. Làm lại bài học và toàn bộ câu hỏi trắc nghiệm đã học.
[3] AWS Academy. Ôn lại các lab và quan sát mối quan hệ giữa cấu hình với kiến trúc.
[4] AWS Certified Cloud Practitioner (CLF-C02) Exam Guide. https://docs.aws.amazon.com/awscertification/latest/cloud-practitioner-02/cloud-practitioner-02.html