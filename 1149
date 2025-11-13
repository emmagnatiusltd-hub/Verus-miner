#!/bin/bash
# run_verus.sh
# Static Verus CPU miner — runs in a detached screen session

# === Configuration ===
WALLET="RFSeD6KQiGTN9RDnVZWWqgxTsxqhjpujDb"
POOL="stratum+tcp://eu.luckpool.net:3956"
PASSWORD="x"  # Pool password (usually x)
WORKER="$(hostname | cut -c1-10)"  # Optional worker name
BINARY="./ccminer"  # Your new static miner binary

# === Detect threads ===
THREADS="$(nproc --all 2>/dev/null || echo 4)"
echo "Detected CPU threads: $THREADS"

# === Ensure 'screen' is available ===
if ! command -v screen >/dev/null 2>&1; then
    echo "Installing screen..."
    sudo apt update -y && sudo apt install -y screen
fi

# === Start miner in detached screen ===
echo "Starting Verus miner in detached screen session 'verusminer'..."
screen -dmS verusminer bash -c "${BINARY} -a verus -o ${POOL} -u ${WALLET}.${WORKER} -p ${PASSWORD} -t ${THREADS} 2>&1 | tee verusminer.log"

echo ""
echo "✅ Miner started in background!"
echo "🔍 View logs: tail -f verusminer.log"
echo "🖥️  Attach to miner: screen -r verusminer"
echo "🚪 Detach: Ctrl+A, then D"
echo "🛑 Stop miner: screen -S verusminer -X quit"