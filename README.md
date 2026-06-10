<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>下見報告書</title>

<!-- Tailwind CSS -->
<link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">

</head>
<body class="bg-gray-100 p-4">

<h1 class="text-2xl font-bold text-center mb-1">株式会社塚腰運送</h1>
<h2 class="text-xl font-bold text-center mb-4">下見報告書</h2>

<form id="form" class="bg-white p-4 rounded-lg shadow space-y-6">
  <input type="hidden" id="editIndex">

  <!-- ========================= -->
  <!-- 基本情報 -->
  <!-- ========================= -->


    <div>
      <label class="font-semibold">ご依頼者様</label>
      <input type="text" id="client" required class="w-full p-3 border rounded">
    </div>

    <div>
      <label class="font-semibold">現場名</label>
      <input type="text" id="siteName" class="w-full p-3 border rounded">
    </div>

    <div>
      <label class="font-semibold">場所（住所）</label>
      <input type="text" id="location" class="w-full p-3 border rounded">

      <button type="button" onclick="openMap()" class="w-full bg-green-600 text-white p-3 rounded-lg mt-2">
        Googleマップで開く
      </button>
    </div>

    <div>
      <label class="font-semibold">現場担当者名</label>
      <input type="text" id="person" class="w-full p-3 border rounded">
    </div>

    <div>
      <label class="font-semibold">現場担当者連絡先（電話番号）</label>
      <input type="tel" id="tel" class="w-full p-3 border rounded">
    </div>

    <div>
      <label class="font-semibold">作業日時</label>
      <input type="datetime-local" id="date" required class="w-full p-3 border rounded">
    </div>
  </div>


  <!-- ========================= -->
  <!-- 作業区分（複数選択） -->
  <!-- ========================= -->
  <div class="space-y-2">
    <h3 class="text-lg font-bold border-b pb-1">作業区分（複数選択可）</h3>

    <div class="flex flex-wrap gap-6 text-lg">
      <label class="flex items-center gap-2">
        <input type="checkbox" name="workType" value="搬入" class="transform scale-125">
        搬入
      </label>

      <label class="flex items-center gap-2">
        <input type="checkbox" name="workType" value="搬出" class="transform scale-125">
        搬出
      </label>

      <label class="flex items-center gap-2">
        <input type="checkbox" name="workType" value="移設" class="transform scale-125">
        移設
      </label>

      <label class="flex items-center gap-2">
        <input type="checkbox" name="workType" value="搬入出" class="transform scale-125">
        搬入出
      </label>
    </div>
  </div>


  <!-- ========================= -->
  <!-- 作業情報 -->
  <!-- ========================= -->
  <div class="space-y-4">
    <h3 class="text-lg font-bold border-b pb-1">作業情報</h3>

    <div>
      <label class="font-semibold">作業内容</label>
      <textarea id="work" class="w-full p-3 border rounded"></textarea>
    </div>

    <div>
      <label class="font-semibold">作業人数</label>
      <input type="number" id="workers" min="1" class="w-full p-3 border rounded">
    </div>
  </div>
  <!-- ========================= -->
  <!-- 必要車両 -->
  <!-- ========================= -->
  <div class="space-y-4">
    <h3 class="text-lg font-bold border-b pb-1">必要車両</h3>

    <!-- 車両リスト（共通スタイル） -->
    <div id="vehicleList" class="space-y-2">

      <!-- 人員輸送車 -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="van">
        <span class="w-40">人員輸送車</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="van" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="van" disabled>
      </div>

      <!-- 2t（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="2t-gate">
        <span class="w-40">2t（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="2t-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="2t-gate" disabled>
      </div>

      <!-- 4t（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="4t-normal">
        <span class="w-40">4t（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="4t-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="4t-normal" disabled>
      </div>

      <!-- 4t（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="4t-gate">
        <span class="w-40">4t（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="4t-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="4t-gate" disabled>
      </div>

      <!-- 6t（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="6t-normal">
        <span class="w-40">6t（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="6t-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="6t-normal" disabled>
      </div>

      <!-- 6t（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="6t-gate">
        <span class="w-40">6t（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="6t-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="6t-gate" disabled>
      </div>

      <!-- 6t（温調） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="6t-temp">
        <span class="w-40">6t（温調）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="6t-temp" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="6t-temp" disabled>
      </div>

      <!-- 8t（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-normal">
        <span class="w-40">8t（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-normal" disabled>
      </div>

      <!-- 8t（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-gate">
        <span class="w-40">8t（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-gate" disabled>
      </div>

      <!-- 8t（温調） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-temp">
        <span class="w-40">8t（温調）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-temp" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-temp" disabled>
      </div>

      <!-- 8t（ユニック） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-unic">
        <span class="w-40">8t（ユニック）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-unic" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-unic" disabled>
      </div>

      <!-- 10t（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="10t-normal">
        <span class="w-40">10t（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="10t-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="10t-normal" disabled>
      </div>

      <!-- 10t（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="10t-gate">
        <span class="w-40">10t（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="10t-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="10t-gate" disabled>
      </div>

      <!-- 10t（温調） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="10t-temp">
        <span class="w-40">10t（温調）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="10t-temp" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="10t-temp" disabled>
      </div>

    </div>
  </div>


  <!-- ========================= -->
  <!-- 機材運搬車 -->
  <!-- ========================= -->
  <div class="space-y-4">
    <h3 class="text-lg font-bold border-b pb-1">機材運搬車</h3>

    <div id="machineList" class="space-y-2">

      <!-- 2t機材（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="2t-m-normal">
        <span class="w-40">2t機材（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="2t-m-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="2t-m-normal" disabled>
      </div>

      <!-- 4t機材（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="4t-m-gate">
        <span class="w-40">4t機材（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="4t-m-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="4t-m-gate" disabled>
      </div>

      <!-- 6t機材（温調） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="6t-m-temp">
        <span class="w-40">6t機材（温調）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="6t-m-temp" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="6t-m-temp" disabled>
      </div>

      <!-- 6t機材（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="6t-m-gate">
        <span class="w-40">6t機材（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="6t-m-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="6t-m-gate" disabled>
      </div>

      <!-- 8t機材（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-m-normal">
        <span class="w-40">8t機材（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-m-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-m-normal" disabled>
      </div>

      <!-- 8t機材（ゲート） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-m-gate">
        <span class="w-40">8t機材（ゲート）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-m-gate" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-m-gate" disabled>
      </div>

      <!-- 8t機材（温調） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-m-temp">
        <span class="w-40">8t機材（温調）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-m-temp" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-m-temp" disabled>
      </div>

      <!-- 8t機材（ユニック） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="8t-m-unic">
        <span class="w-40">8t機材（ユニック）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="8t-m-unic" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="8t-m-unic" disabled>
      </div>

      <!-- 10t機材（通常） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="10t-m-normal">
        <span class="w-40">10t機材（通常）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="10t-m-normal" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="10t-m-normal" disabled>
      </div>

      <!-- 10t機材（温調） -->
      <div class="flex items-center gap-3">
        <input type="checkbox" class="vehicle-check" data-id="10t-m-temp">
        <span class="w-40">10t機材（温調）</span>
        <input type="number" class="vehicle-count w-24 p-2 border rounded bg-gray-200" data-id="10t-m-temp" disabled>
        <span>台</span>
        <input type="text" class="vehicle-note flex-1 p-2 border rounded bg-gray-200" placeholder="備考" data-id="10t-m-temp" disabled>
      </div>

    </div>
  </div>
  <!-- ========================= -->
  <!-- 現場情報 -->
  <!-- ========================= -->
  <div class="space-y-4">
    <h3 class="text-lg font-bold border-b pb-1">現場情報</h3>

    <div>
      <label class="font-semibold">搬入経路</label>
      <textarea id="route" class="w-full p-3 border rounded"></textarea>
    </div>

    <div>
      <label class="font-semibold">必要資材</label>
      <textarea id="danger" class="w-full p-3 border rounded"></textarea>
    </div>

    <div>
      <label class="font-semibold">駐車位置</label>
      <textarea id="parking" class="w-full p-3 border rounded"></textarea>
    </div>

    <div>
      <label class="font-semibold">備考</label>
      <textarea id="note" class="w-full p-3 border rounded"></textarea>
    </div>
  </div>


  <!-- ========================= -->
  <!-- 写真添付 -->
  <!-- ========================= -->
  <div class="space-y-2">
    <h3 class="text-lg font-bold border-b pb-1">写真添付</h3>
    <input type="file" id="photos" multiple class="w-full p-3 border rounded">
  </div>


  <!-- ========================= -->
  <!-- ボタン -->
  <!-- ========================= -->
  <div class="flex flex-wrap gap-3 mt-4">
    <button type="button" onclick="saveData()" class="px-4 py-2 bg-blue-600 text-white rounded">一時保存</button>
    <button type="button" onclick="loadData()" class="px-4 py-2 bg-green-600 text-white rounded">保存データ読込</button>
    <button type="button" onclick="generateMail()" class="px-4 py-2 bg-indigo-600 text-white rounded">メール本文生成</button>
    <button type="button" onclick="window.print()" class="px-4 py-2 bg-gray-700 text-white rounded">印刷</button>

    <button type="button" onclick="clearForm()" class="px-4 py-2 bg-red-500 text-white rounded">入力内容クリア</button>
    <button type="button" onclick="deleteSavedData()" class="px-4 py-2 bg-yellow-600 text-white rounded">保存データ削除</button>
    <button type="button" onclick="sendMail()" class="px-4 py-2 bg-purple-600 text-white rounded">メール送信</button>
  </div>


  <!-- ========================= -->
  <!-- メール本文プレビュー -->
  <!-- ========================= -->
  <div class="mt-4">
    <label class="font-semibold">メール本文プレビュー</label>
    <textarea id="mailPreview" class="w-full p-3 border rounded h-48" readonly></textarea>
  </div>

</form>


<!-- ========================= -->
<!-- JavaScript（最適化済み） -->
<!-- ========================= -->
<script>

/* Googleマップ */
function openMap() {
  const address = location.value;
  if (address) {
    window.open("https://www.google.com/maps/search/?api=1&query=" + encodeURIComponent(address));
  }
}

/* 車両チェックで入力欄ON/OFF */
document.querySelectorAll(".vehicle-check").forEach(cb => {
  cb.addEventListener("change", () => {
    const id = cb.dataset.id;
    const count = document.querySelector(`.vehicle-count[data-id="${id}"]`);
    const note = document.querySelector(`.vehicle-note[data-id="${id}"]`);
    const enable = cb.checked;

    [count, note].forEach(el => {
      el.disabled = !enable;
      el.classList.toggle("bg-gray-200", !enable);
      el.classList.toggle("bg-white", enable);
    });
  });
});


/* 一時保存 */
function saveData() {
  const data = {
    client: client.value,
    date: date.value,
    location: location.value,
    siteName: siteName.value,
    person: person.value,
    tel: tel.value,
    work: work.value,
    workers: workers.value,
    route: route.value,
    danger: danger.value,
    parking: parking.value,
    note: note.value,
    workTypes: [...document.querySelectorAll('input[name="workType"]:checked')].map(cb => cb.value),
    vehicles: []
  };

  document.querySelectorAll(".vehicle-check").forEach(cb => {
    const id = cb.dataset.id;
    data.vehicles.push({
      id,
      checked: cb.checked,
      count: document.querySelector(`.vehicle-count[data-id="${id}"]`).value,
      note: document.querySelector(`.vehicle-note[data-id="${id}"]`).value
    });
  });

  localStorage.setItem("previewData", JSON.stringify(data));
  alert("保存しました");
}


/* 保存データ読込 */
function loadData() {
  const raw = localStorage.getItem("previewData");
  if (!raw) return alert("保存データがありません");

  const data = JSON.parse(raw);

  client.value = data.client || "";
  date.value = data.date || "";
  location.value = data.location || "";
  siteName.value = data.siteName || "";
  person.value = data.person || "";
  tel.value = data.tel || "";
  work.value = data.work || "";
  workers.value = data.workers || "";
  route.value = data.route || "";
  danger.value = data.danger || "";
  parking.value = data.parking || "";
  note.value = data.note || "";

  /* 作業区分 */
  document.querySelectorAll('input[name="workType"]').forEach(cb => {
    cb.checked = data.workTypes?.includes(cb.value);
  });

  /* 車両 */
  if (data.vehicles) {
    data.vehicles.forEach(v => {
      const cb = document.querySelector(`.vehicle-check[data-id="${v.id}"]`);
      const count = document.querySelector(`.vehicle-count[data-id="${v.id}"]`);
      const note = document.querySelector(`.vehicle-note[data-id="${v.id}"]`);

      if (!cb) return;

      cb.checked = v.checked;
      count.value = v.count;
      note.value = v.note;

      const enable = v.checked;
      [count, note].forEach(el => {
        el.disabled = !enable;
        el.classList.toggle("bg-gray-200", !enable);
        el.classList.toggle("bg-white", enable);
      });
    });
  }

  alert("保存データを読み込みました");
}


/* メール本文生成 */
function generateMail() {
  let text = "";

  text += "【下見報告書】\n\n";
  text += "■ご依頼者様\n" + client.value + "\n\n";
  text += "■作業日時\n" + date.value + "\n\n";
  text += "■場所\n" + location.value + "\n\n";
  text += "■現場名\n" + siteName.value + "\n\n";
  text += "■担当者\n" + person.value + "\n\n";
  text += "■連絡先\n" + tel.value + "\n\n";

  /* 作業区分 */
  const workTypes = [...document.querySelectorAll('input[name="workType"]:checked')].map(cb => cb.value);
  text += "■作業区分\n" + (workTypes.length ? workTypes.join("・") : "未選択") + "\n\n";

  text += "■作業内容\n" + work.value + "\n\n";
  text += "■作業人数\n" + workers.value + " 名\n\n";

  text += "■必要車両\n";
  document.querySelectorAll(".vehicle-check").forEach(cb => {
    const id = cb.dataset.id;
    const label = cb.parentElement.querySelector("span").textContent;
    const count = document.querySelector(`.vehicle-count[data-id="${id}"]`).value;
    const note = document.querySelector(`.vehicle-note[data-id="${id}"]`).value;

    if (cb.checked && count) {
      text += "・" + label + "：" + count + "台";
      if (note) text += "（" + note + "）";
      text += "\n";
    }
  });

  text += "\n■搬入経路\n" + route.value + "\n\n";
  text += "■危険ポイント\n" + danger.value + "\n\n";
  text += "■駐車位置\n" + parking.value + "\n\n";
  text += "■備考\n" + note.value + "\n\n";

  mailPreview.value = text;
  alert("メール本文を生成しました");
}


/* 入力内容クリア */
function clearForm() {
  form.reset();

  document.querySelectorAll(".vehicle-count, .vehicle-note").forEach(el => {
    el.value = "";
    el.disabled = true;
    el.classList.add("bg-gray-200");
    el.classList.remove("bg-white");
  });

  mailPreview.value = "";
  alert("入力内容をクリアしました");
}


/* 保存データ削除 */
function deleteSavedData() {
  localStorage.removeItem("previewData");
  alert("保存データを削除しました");
}


/* メール送信 */
function sendMail() {
  const body = encodeURIComponent(mailPreview.value);
  const subject = encodeURIComponent("下見報告書");
  window.location.href = `mailto:?subject=${subject}&body=${body}`;
}

</script>

</body>
</html>
