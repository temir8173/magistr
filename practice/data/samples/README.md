# Учебные образцы снимков с БПЛА

Два снимка из открытых датасетов проекта ICAERUS с разметкой в формате YOLO.
Используются в модуле 0–1 (проверка готовой модели) и в модуле 2 (разбор формата разметки).

| Файл | Что на снимке | Объектов в разметке | Источник |
|---|---|---|---|
| `aerial_cattle.jpg` + `.txt` | пастбище с коровами, вид сверху (ферма Mauron, Франция) | 53 | Cattle, файл `DJI_20230605184604_0026_V` |
| `aerial_sheep.jpg` + `.txt` | отара овец, вид сверху | 50 | Sheep, файл `DJI_20251010112840_0102_V` (папка `test/Nadir_only`) |

Снимки уменьшены до ширины 2400 px (оригиналы 4000 и 4032 px), чтобы не
раздувать репозиторий. Разметка YOLO хранит координаты в долях от размеров
снимка (0–1), поэтому после уменьшения она остаётся верной.

## Авторство и лицензия

Оба датасета распространяются по лицензии
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): использовать можно
при указании авторов.

- Lebreton A., Helary L. *Drone images and their annotations of grazing cows.*
  Zenodo, 2024. DOI: [10.5281/zenodo.11048412](https://doi.org/10.5281/zenodo.11048412)
- Lebreton A., de Brito A., Blaise E., Jegorel T., Goin L., Grisot P.-G.,
  Nicolas E., Helary L. *Drone images and their annotations of sheep in various
  conditions (for computer vision purpose).* Zenodo, 2026.
  DOI: [10.5281/zenodo.18889623](https://doi.org/10.5281/zenodo.18889623)

Изменения: снимки уменьшены, разметка не изменялась.
