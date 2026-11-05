# Lab 0 — Inventory

Пара: Sergaziyev (работал один, напарник не участвовал)  Первый водитель: Sergaziyev
Машина: MacBook Air (Apple M2), macOS, без виртуальной машины
Дата: 05.11.2026, 17:00

## Что я сделал

Все значения получены только из терминала, окно «Об этом Mac» не открывалось.

```bash
sysctl -n machdep.cpu.brand_string
sysctl hw.physicalcpu hw.logicasysctl hw.physicalcpu hw.logicasysctl hw.physicalcmsize
system_profiler SPStorageDataType SPNVMeDataType
diskutil info /
df -h /
df -h /System/Volumes/Data
system_profiler SPHardwareDataType | grep -i -E "firmware|model"
sysctl kern.hv_support
sysctl machdep.cpu.features
sw_vers; uname -m
```

## Результат

| Что | Значение | Где я его получил |
|---|---|---|
| Процессор | Apple M2 | `sysctl -n machdep.cpu.brand_string` |
| Ядра / потоки | 8 физических / 8 логических (SMT нет) | `sysctl hw.physicalcpu hw.logicalcpu` |
| Память, объём | 16 ГБ (17 179 869 184 байт) | `sysctl hw.memsize` |
| Память, тип и модули | LPDDR5, Hynix. Одна запись, слотов и сменных модулей нет: память распаяна, апгрейд невозможен | `system_profiler SPMemoryDataType` |
| Память, скорость | Команда не показывает частоту на Apple Silicon, поэтому значение не изм| Память, скорость | Комаype` || Памят�модель | APPLE SSD AP0256Z, 251 ГБ, GPT | `system_profiler SPNVMeDataType` |
| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `syst| Диск, тиorageDa| Диск, тип |одно на томе для ВМ | 178,86 ГБ свободно из 245,11 Г�| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `syst|taT| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `syst| Диск, тиorageDa| Диск, тип |одно на т�е| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `syst| Диск, т�о�| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `syst| Диск, тиorageDa| Диск, тип |одно на томе для ВМ | 178,86 ГБ свободно из 245,11 Г�| Диск, тип | SSD, NVMe (Apple Fabricо виртуализацию: проверка `VMX` (термин Intel) на M2 ничего не вывела, потому что в архитектуре ARM такого флага нет. Поддержку показывает `kern.hv_support`.

Важное для следующих лаб: процессор ARM, поэтому нужны ARM64-образы (Ubuntu Server ARM64, Windows 11 ARM). Для Lab 1 и Lab 2 надо уточнить у преподавателя, подойдёт ли это.

## Что не сработало в первый раз

1. **Команды Git в неправильной папке.** `git status`, `git add`, `git commit`, `git push` я запускал в домашней папке `~` и получил `fatal: not a git repository`. Git работает только внутри папки репозитория. Решение: `cd ~/osarch-sergaziyev` и повторить.
2. **Push не прошёл по паролю.** GitHub ответил `Password authentication is not supported for Git operations`. Пароль аккаунта больше не принимается, нужен Personal Access Token. Решение: создать токен (Settings → Developer settings → Tokens, право `repo`) и вставить его вместо пароля.
3. **Смена логина GitHub.** Я переименовал аккаунт, и старый адрес репозитория перестал быть правильным. Решение: `gi3. **Смена логина GitHub.** Я переиvdias/osarch-sergaziyev.git`.
4. **Объём диска и свободное место.** Сначала легко взять число 245 ГБ, но это ёмкость, а не свободное место. Свободное место на томе: 178,86 ГБ.

## Доказательства

- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evid [evidence/virtualization.txt](evidence/virtualization.txt) — `kern.hv_support: 1`.
- [evidence/os.txt](evidence/os.txt) — версия macOS и архитектура arm64.
