const decreaseBtn = document.getElementById('decrease');
const resetBtn = document.getElementById('reset');
const increaseBtn = document.getElementById('increase');
const bwButton = document.getElementById('bwButton');

[decreaseBtn, resetBtn, increaseBtn, bwButton].forEach(btn => {
    btn.addEventListener('click', e => {
        e.preventDefault();  // ✅ prevents default action (like submitting a form)
        e.stopPropagation(); // ✅ stops bubbling to dropdown toggle
    });
});

const MIN = 80;
const MAX = 150;
const STEP = 10;
const STORAGE_KEY = 'fontScale';
const BW_KEY = 'bwActive';

let scale = parseInt(localStorage.getItem(STORAGE_KEY)) || 100;
applyScale();

decreaseBtn.addEventListener('click', e => {
    e.preventDefault();
    adjustScale(-STEP);
});

increaseBtn.addEventListener('click', e => {
    e.preventDefault();
    adjustScale(+STEP);
});

resetBtn.addEventListener('click', e => {
    e.preventDefault();
    scale = 100;
    applyScale();
    saveScale();
});

function adjustScale(delta) {
    scale = Math.min(MAX, Math.max(MIN, scale + delta));
    applyScale();
    saveScale();
}

function applyScale() {
    // Remove all font-scale classes
    document.documentElement.className = document.documentElement.className
        .split(' ')
        .filter(cls => !/^font-scale-\d+$/.test(cls))
        .join(' ')
        .trim();
    document.documentElement.classList.add(`font-scale-${scale}`);
}

function saveScale() {
    localStorage.setItem(STORAGE_KEY, scale);
}

// Toggle bw-active and save state
bwButton.addEventListener('click', function (e) {
    e.preventDefault();
    document.body.classList.toggle('bw-active');
    const isActive = document.body.classList.contains('bw-active');
    localStorage.setItem(BW_KEY, isActive ? 'true' : 'false');
});

// Restore bw-active on load
document.addEventListener('DOMContentLoaded', () => {
    const bwActive = localStorage.getItem(BW_KEY);
    if (bwActive === 'true') {
        document.body.classList.add('bw-active');
    }
});
