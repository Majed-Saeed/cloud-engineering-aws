# AWS Multi-AZ Architecture

Basic AWS Multi-AZ architecture concept for improving availability and reducing single points of failure.

---

## Services

- Amazon VPC
- EC2
- Application Load Balancer (ALB)
- Security Groups
- Route Tables
- Internet Gateway
- Amazon RDS (Concept)

---

## Architecture

```text
Internet
    ↓
Application Load Balancer
    ↓
EC2 Instances (Multiple AZs)
    ↓
Database Layer

export default function App() {
  return (
    <div
      style={{
        background: "#09131F",
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
        minHeight: "100vh",
        padding: "0",
      }}
    >
      <svg
        viewBox="0 0 1200 630"
        xmlns="http://www.w3.org/2000/svg"
        style={{
          width: "100%",
          maxWidth: "1200px",
          fontFamily: "'Segoe UI', system-ui, -apple-system, sans-serif",
        }}
      >
        <defs>
          {/* Arrow: blue */}
          <marker id="ab" markerWidth="9" markerHeight="7" refX="8" refY="3.5" orient="auto">
            <polygon points="0 0, 9 3.5, 0 7" fill="#4A9EE8" />
          </marker>
          {/* Arrow: orange */}
          <marker id="ao" markerWidth="9" markerHeight="7" refX="8" refY="3.5" orient="auto">
            <polygon points="0 0, 9 3.5, 0 7" fill="#FF9900" />
          </marker>
          {/* Dot grid */}
          <pattern id="dots" width="28" height="28" patternUnits="userSpaceOnUse">
            <circle cx="14" cy="14" r="0.9" fill="#162030" />
          </pattern>
          {/* Soft glow for title */}
          <filter id="glow">
            <feGaussianBlur in="SourceGraphic" stdDeviation="3" result="b" />
            <feMerge>
              <feMergeNode in="b" />
              <feMergeNode in="SourceGraphic" />
            </feMerge>
          </filter>
        </defs>

        {/* ── BACKGROUND ─────────────────────────────────────── */}
        <rect width="1200" height="630" fill="#09131F" />
        <rect width="1200" height="630" fill="url(#dots)" />

        {/* Subtle horizontal accent line below title */}
        <line x1="0" y1="84" x2="1200" y2="84" stroke="#FF9900" strokeWidth="1.5" opacity="0.15" />

        {/* ── TITLE ──────────────────────────────────────────── */}
        <text
          x="600" y="40"
          textAnchor="middle"
          fill="#FF9900"
          fontSize="27"
          fontWeight="700"
          letterSpacing="0.8"
          filter="url(#glow)"
        >
          AWS Multi-AZ Architecture
        </text>
        <text
          x="600" y="66"
          textAnchor="middle"
          fill="#6A8BAA"
          fontSize="13"
          letterSpacing="0.2"
        >
          High Availability · No Single Point of Failure · Automatic Failover
        </text>

        {/* ── AWS REGION BOX ─────────────────────────────────── */}
        <rect
          x="40" y="90" width="1120" height="510"
          rx="8" fill="none"
          stroke="#FF9900" strokeWidth="1.4" strokeDasharray="9 5"
          opacity="0.7"
        />
        {/* Region label badge */}
        <rect x="50" y="83" width="192" height="20" fill="#09131F" />
        <text x="58" y="97" fill="#FF9900" fontSize="12" fontWeight="600" opacity="0.9">
          AWS Region: us-east-1
        </text>

        {/* ── INTERNET / USERS ───────────────────────────────── */}
        {/* Pill-shaped "Users" badge at top-center */}
        <rect x="462" y="106" width="276" height="40" rx="20" fill="#0C1E30" stroke="#4A9EE8" strokeWidth="1.4" />
        {/* Wifi-like icon dots */}
        <circle cx="490" cy="126" r="3" fill="#4A9EE8" opacity="0.5" />
        <circle cx="500" cy="126" r="3" fill="#4A9EE8" opacity="0.75" />
        <circle cx="510" cy="126" r="3" fill="#4A9EE8" />
        <text x="530" y="131" fill="#F0F4FF" fontSize="13" fontWeight="500">
          Users / Internet Traffic
        </text>

        {/* ── ARROW: Internet → ALB ──────────────────────────── */}
        <line x1="600" y1="146" x2="600" y2="192" stroke="#4A9EE8" strokeWidth="2" markerEnd="url(#ab)" />

        {/* ── APPLICATION LOAD BALANCER ──────────────────────── */}
        <rect x="418" y="196" width="364" height="62" rx="6" fill="#0D2038" stroke="#4A9EE8" strokeWidth="1.5" />
        {/* ALB left color bar */}
        <rect x="418" y="196" width="5" height="62" rx="3" fill="#4A9EE8" opacity="0.9" />
        {/* ALB tag */}
        <rect x="428" y="206" width="36" height="16" rx="4" fill="#4A9EE8" opacity="0.18" />
        <text x="446" y="218" textAnchor="middle" fill="#4A9EE8" fontSize="9.5" fontWeight="700">ALB</text>
        {/* ALB text */}
        <text x="600" y="221" textAnchor="middle" fill="#F0F4FF" fontSize="14" fontWeight="600">
          Application Load Balancer
        </text>
        <text x="600" y="241" textAnchor="middle" fill="#4A9EE8" fontSize="11">
          Distributes incoming traffic across both Availability Zones
        </text>
        {/* healthy dot */}
        <circle cx="760" cy="212" r="5" fill="#22C55E" />
        <text x="769" y="216" fill="#22C55E" fontSize="9.5" fontWeight="500">Healthy</text>

        {/* ── ARROWS: ALB → EC2s ─────────────────────────────── */}
        {/* Left (AZ1a): from ALB bottom-left to EC2 top-center */}
        <path
          d="M 492 258 L 314 308"
          stroke="#4A9EE8" strokeWidth="2" fill="none"
          markerEnd="url(#ab)" strokeDasharray="6 3"
        />
        {/* Right (AZ1b): symmetric */}
        <path
          d="M 708 258 L 886 308"
          stroke="#4A9EE8" strokeWidth="2" fill="none"
          markerEnd="url(#ab)" strokeDasharray="6 3"
        />
        {/* Small "routes to" labels on arrows */}
        <rect x="390" y="273" width="68" height="14" fill="#09131F" />
        <text x="424" y="284" textAnchor="middle" fill="#4A9EE8" fontSize="9.5">50% traffic</text>
        <rect x="742" y="273" width="68" height="14" fill="#09131F" />
        <text x="776" y="284" textAnchor="middle" fill="#4A9EE8" fontSize="9.5">50% traffic</text>

        {/* ═══════════════════════════════════════════════════
            AVAILABILITY ZONE 1a
        ═══════════════════════════════════════════════════ */}
        <rect
          x="56" y="290" width="518" height="272"
          rx="7" fill="#0B1C2C" stroke="#2563EB"
          strokeWidth="1.5" strokeDasharray="6 3"
        />
        {/* AZ label */}
        <rect x="56" y="282" width="202" height="18" fill="#09131F" />
        <text x="64" y="296" fill="#60A5FA" fontSize="12" fontWeight="700">
          Availability Zone: us-east-1a
        </text>

        {/* ── EC2 · AZ1a ─────────────────────────────── */}
        <rect x="78" y="312" width="474" height="90" rx="5" fill="#0D1F33" stroke="#2563EB" strokeWidth="1.2" />
        {/* Server icon: stacked bars */}
        <rect x="96" y="332" width="30" height="7" rx="2" fill="#3B82F6" />
        <rect x="96" y="343" width="30" height="7" rx="2" fill="#3B82F6" opacity="0.65" />
        <rect x="96" y="354" width="30" height="7" rx="2" fill="#3B82F6" opacity="0.35" />
        <circle cx="120" cy="335.5" r="2.2" fill="#22C55E" />
        {/* EC2 text */}
        <text x="140" y="340" fill="#F0F4FF" fontSize="13.5" fontWeight="600">Amazon EC2 Instance</text>
        <text x="140" y="358" fill="#6A8BAA" fontSize="11">Application Server  ·  us-east-1a</text>
        <text x="140" y="374" fill="#6A8BAA" fontSize="11">Type: t3.medium  ·  State: running</text>
        {/* Status badge */}
        <rect x="488" y="322" width="52" height="18" rx="9" fill="#14532D" />
        <circle cx="501" cy="331" r="3.5" fill="#22C55E" />
        <text x="521" y="335" textAnchor="middle" fill="#22C55E" fontSize="9" fontWeight="600">Active</text>

        {/* ── RDS Primary · AZ1a ─────────────────────── */}
        <rect x="78" y="422" width="474" height="90" rx="5" fill="#0D1F33" stroke="#7C3AED" strokeWidth="1.2" />
        {/* DB cylinder icon */}
        <ellipse cx="111" cy="458" rx="15" ry="5" fill="#7C3AED" opacity="0.8" />
        <rect x="96" y="458" width="30" height="18" fill="#7C3AED" opacity="0.35" />
        <ellipse cx="111" cy="476" rx="15" ry="5" fill="#7C3AED" opacity="0.6" />
        {/* RDS text */}
        <text x="140" y="450" fill="#F0F4FF" fontSize="13.5" fontWeight="600">Amazon RDS  ·  Primary</text>
        <text x="140" y="468" fill="#6A8BAA" fontSize="11">MySQL 8.0  ·  Read / Write</text>
        <text x="140" y="484" fill="#6A8BAA" fontSize="11">Receives all write operations</text>
        {/* Status badge */}
        <rect x="488" y="432" width="52" height="18" rx="9" fill="#14532D" />
        <circle cx="501" cy="441" r="3.5" fill="#22C55E" />
        <text x="521" y="445" textAnchor="middle" fill="#22C55E" fontSize="9" fontWeight="600">Active</text>

        {/* ═══════════════════════════════════════════════════
            AVAILABILITY ZONE 1b
        ═══════════════════════════════════════════════════ */}
        <rect
          x="626" y="290" width="518" height="272"
          rx="7" fill="#0B1C2C" stroke="#2563EB"
          strokeWidth="1.5" strokeDasharray="6 3"
        />
        {/* AZ label */}
        <rect x="626" y="282" width="202" height="18" fill="#09131F" />
        <text x="634" y="296" fill="#60A5FA" fontSize="12" fontWeight="700">
          Availability Zone: us-east-1b
        </text>

        {/* ── EC2 · AZ1b ─────────────────────────────── */}
        <rect x="648" y="312" width="474" height="90" rx="5" fill="#0D1F33" stroke="#2563EB" strokeWidth="1.2" />
        <rect x="666" y="332" width="30" height="7" rx="2" fill="#3B82F6" />
        <rect x="666" y="343" width="30" height="7" rx="2" fill="#3B82F6" opacity="0.65" />
        <rect x="666" y="354" width="30" height="7" rx="2" fill="#3B82F6" opacity="0.35" />
        <circle cx="690" cy="335.5" r="2.2" fill="#22C55E" />
        <text x="710" y="340" fill="#F0F4FF" fontSize="13.5" fontWeight="600">Amazon EC2 Instance</text>
        <text x="710" y="358" fill="#6A8BAA" fontSize="11">Application Server  ·  us-east-1b</text>
        <text x="710" y="374" fill="#6A8BAA" fontSize="11">Type: t3.medium  ·  State: running</text>
        <rect x="1058" y="322" width="52" height="18" rx="9" fill="#14532D" />
        <circle cx="1071" cy="331" r="3.5" fill="#22C55E" />
        <text x="1091" y="335" textAnchor="middle" fill="#22C55E" fontSize="9" fontWeight="600">Active</text>

        {/* ── RDS Standby · AZ1b ─────────────────────── */}
        <rect x="648" y="422" width="474" height="90" rx="5" fill="#0D1F33" stroke="#7C3AED" strokeWidth="1.2" />
        <ellipse cx="681" cy="458" rx="15" ry="5" fill="#7C3AED" opacity="0.8" />
        <rect x="666" y="458" width="30" height="18" fill="#7C3AED" opacity="0.35" />
        <ellipse cx="681" cy="476" rx="15" ry="5" fill="#7C3AED" opacity="0.6" />
        <text x="710" y="450" fill="#F0F4FF" fontSize="13.5" fontWeight="600">Amazon RDS  ·  Standby Replica</text>
        <text x="710" y="468" fill="#6A8BAA" fontSize="11">MySQL 8.0  ·  Sync Replication</text>
        <text x="710" y="484" fill="#6A8BAA" fontSize="11">Promotes to Primary on AZ failure</text>
        <rect x="1058" y="432" width="64" height="18" rx="9" fill="#451A03" />
        <circle cx="1071" cy="441" r="3.5" fill="#F59E0B" />
        <text x="1093" y="445" textAnchor="middle" fill="#F59E0B" fontSize="9" fontWeight="600">Standby</text>

        {/* ── SYNC REPLICATION ARROW ─────────────────────────── */}
        {/* RDS Primary right edge: x = 78+474 = 552 */}
        {/* RDS Standby left edge: x = 648 */}
        {/* Center: y = 422 + 45 = 467 */}
        <line
          x1="552" y1="467" x2="648" y2="467"
          stroke="#FF9900" strokeWidth="2"
          strokeDasharray="5 2"
          markerEnd="url(#ao)"
        />
        {/* Arrow label */}
        <rect x="554" y="455" width="92" height="15" fill="#09131F" />
        <text x="600" y="467" textAnchor="middle" fill="#FF9900" fontSize="10" fontWeight="600">
          Sync Replication
        </text>

        {/* ── BOTTOM NOTE (inside region box) ───────────────── */}
        <text
          x="600" y="576"
          textAnchor="middle"
          fill="#3A5A7A"
          fontSize="11.5"
          fontStyle="italic"
        >
          If one AZ goes down, traffic automatically shifts to the healthy zone — zero manual steps needed
        </text>

        {/* ── FOOTER ─────────────────────────────────────────── */}
        <line x1="80" y1="612" x2="1120" y2="612" stroke="#162030" strokeWidth="1" />
        <text x="600" y="626" textAnchor="middle" fill="#2A4460" fontSize="10.5" letterSpacing="1">
          AWS  ·  Multi-AZ  ·  High Availability  ·  Auto Failover  ·  No Single Point of Failure
        </text>
      </svg>
    </div>
  );
}

