# Example: Phase Kickoff Packet

この例は、steady state を維持したまま broad phase 候補を整理する pre-lane packet の記入例です。

ここで重要なのは、phase 自体を開くことではなく、次を固定することです。

- なぜその phase 候補が見えているのか
- それでも今は自動的に reopen しない理由
- 開くならどの first bounded slice から始めるべきか
- 開かないならどの posture を維持するか

対応テンプレート:

- `../../templates/phase_kickoff_packet_template.md`
