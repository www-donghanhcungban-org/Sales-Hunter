# PROJECT STATUS — Sales-Hunter

## Snapshot hiện tại

- Ngày cập nhật: 2026-10-09
- Base branch: `bootstrap/base`
- Base hiện tại: `98c46770565fd6fae5125a5fe403104732c708a3`
- Base đã có skeleton Phase 1–6, #35 audit, #36 packaging, #37 giá/dashboard, #38 integrity, #40 projection, #39 local auth, #41 revision/transaction/history, #42 facts/eligibility/grounded payload, #43 durable publishing (intent/lease/reconcile/recall, chỉ transport fake) và #47 audit từng dòng 2026-10-09 (ranh giới HTTP, JSON chặt, fencing worker/recall, urllib3 2.8.0, throttle đăng nhập, audit dependency hàng tuần) và #48 allowlist URL version hóa ADR-0011 (`config/url-allowlist.v1.json` rỗng, fail-closed; builder/manual flow/API nhập candidate bắt buộc policy).
- Chưa production/staging thực, chưa client nền tảng thật, chưa đổi DNS/secret hoặc chạy migration dữ liệu người dùng. Dry-run, pause toàn cục mặc định và review vẫn là cổng bắt buộc.

## Nhánh tích hợp Đồng Hành

- `feat/dhcb-platform-pilot-20260926`: WSGI pilot riêng, dashboard chỉ đọc với xác thực
  độc lập, cấu hình systemd/Access và hợp đồng lối vào từ website Đồng Hành.
- Đây là implementation nguồn trên nhánh, không phải đã merge hoặc đã online.
- 12 test mới; bản chạy chẩn đoán local phải đối chiếu session. CI khóa dependency,
  human T4 trên diff cuối và ADR0011 chưa được thay bằng kết quả local.
- Xem [runbook](docs/PLATFORM-PILOT.md), [ADR0011](docs/adr/0011-platform-read-only-pilot.md)
  và [task pack](docs/task-packs/2026-09-26-platform-pilot.md).
- Pilot mở snapshot Sales bằng SQLite read-only; không migration/ghi DB, không endpoint
  approve/publish, không cấp quyền từ cookie/identity/billing Learning. API operator cũ
  tiếp tục loopback-only. Không gọi view này là operator production đầy đủ.

## Việc còn lại

- [Audit từng dòng 2026-10-09](docs/sessions/2026-10-09-line-audit.md) với [task pack](docs/task-packs/2026-10-09-audit-hardening.md); [audit gốc 2026-09-25](docs/audits/2026-09-25/README.md) giữ nguyên; [ma trận 27 mục](docs/implementation/2026-09-25/execution-matrix.md) là checkpoint lịch sử.
- Việc còn lại cần ADR/owner: analytics bền vững, identity/roles trước staging ngoài; thêm domain nền tảng thật vào allowlist cần nguồn chính thức + ngày kiểm chứng (owner). Luồng legacy chỉ kiểm HTTPS đã đóng bởi ADR-0011 ([#48](https://github.com/www-donghanhcungban-org/Sales-Hunter/pull/48), đã merge); [session](docs/sessions/2026-10-09-url-allowlist.md).
- Analytics/ledger, operator form/CSV/inbox/bulk workflow, lịch sử giá, identity nhiều người dùng, server/TLS production và restore drill chưa hoàn tất. Publishing dùng manual/fake; không suy quyền API/account từ test mô phỏng.
- Django/PostgreSQL cần ADR được chấp nhận; chưa tự thay stdlib/SQLite. ADR0003/0004 có điều kiện, checklist/evidence vẫn bắt buộc trước cutover.
- Human review, khóa/audit dependency triển khai, xác nhận VPS/Cloudflare, cài staging, HTTPS/Access read-back và restore/rollback drill còn là cổng trước kích hoạt. Lối vào website mặc định chưa mở. Mở subdomain không đồng nghĩa bật publisher.

## Bằng chứng lịch sử và resume

[Ma trận audit](docs/implementation/2026-09-25/execution-matrix.md) và
[audit gốc](docs/audits/2026-09-25/README.md) là lịch sử theo checkpoint, không dùng trạng
thái PR cũ trong đó thay GitHub hiện hành. Đọc AGENTS/TRAPS/ARCHITECTURE/CODEMAP trước khi
đổi code. Không push/force base, không bypass test/human review, không giả live receipt.
