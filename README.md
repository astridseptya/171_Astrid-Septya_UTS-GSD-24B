# UTS Graf Sains Data - Recommender System (Neo4j & Python)

**Nama** : Astrid Septya Regita P.  
**NIM**  : 24031554171  
---

### Ringkasan Pengerjaan:
1. **Periode Filter Waktu**
   - **Fold Training (P1)**: 16 Juli 2015 s.d. 31 Juli 2015 (`data/events_p1.csv`)
   - **Fold Testing (P2)** : 01 Agustus 2015 s.d. 15 Agustus 2015 (`data/events_p2.csv`)
2. **Model Graf**:
   - Database: Neo4j (Bipartite Graph: Visitor & Item), hanya data P1 yang diimpor
   - Komposisi: 199.899 Visitor, 88.699 Item, 364.206 relasi (VIEWED 351.830, ADDED_TO_CART 9.263, BOUGHT 3.113)
   - Matriks interaksi User x Item berukuran 199.899 x 88.699 dengan sparsity 99,9984 %
   - Proyeksi Terbaik: Item-to-Item Projection (ruang pasangan 80,3 % lebih kecil dibanding proyeksi User-to-User, dengan catatan 48,2 % item terisolasi)
3. **Similarity**: cosine similarity antar-item (Python), pembanding Jaccard (Cypher), 5 item termirip ditulis ke graf sebagai relasi `SIMILAR_TO` (item acuan: 149275)
4. **Hasil Evaluasi Rekomendasi k-NN (User 1349456, k = 5, seed = 71)**:
   - **Item yang diiklankan (3 teratas)**: 59953, 245084, 179859
   - **Hit@5**  : **0.0000** (item di masa depan P2, yaitu 67463, tidak masuk 5 rekomendasi teratas)
   - **NDCG@5** : **0.0000**
   - Rata-rata pada 200 user: Hit@5 = 0.0250 dan NDCG@5 = 0.0098

### Catatan
- Nilai evaluasi rendah karena data sangat jarang (81,7 % user hanya berinteraksi dengan 1 item) dan hanya 6.913 visitor yang muncul di P1 dan P2.
- Kunci jawaban evaluasi: item yang disentuh user di P2, yang belum pernah disentuh di P1 dan ada di katalog P1.
