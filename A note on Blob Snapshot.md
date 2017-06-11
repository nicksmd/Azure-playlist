* Snapshot là phiên bản read-only của một blob được tạo ra tại 1 thời điểm nhất định.
* Snapshot giống y hệt blob gốc (metadata, properties) ngoại trừ URI có thêm DateTime value
chỉ thời điểm snapshot được tạo ra.
```javascript
http://storagesample.core.blob.windows.net/mydrives/myvhd
http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2017-03-09T01:42:34.9360000Z
```
* Snapshot có thể được copy để tạo ra 1 blob mới hoặc có thể được promote để ghi đè
lên blob gốc. Khi đó metadata của blob gốc bị ghi đè bởi metadata của snapshot.
* Khi copy blob gốc thì các snapshot của nó ko bị copy theo
* Không thể xóa 1 blob gốc khi mà các nó vẫn còn snapshot. Để xóa được thì ta phải
xóa cả các snapshot của nó.
* Chi phí của snapshot:

    - trường hợp 1:

        ![](https://docs.microsoft.com/en-us/azure/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

        tạo 1 snapshot, ko thay đổi blob gốc => bị tính phí 3 blocks 1,2,3.
    - trường hợp 2:

        ![](https://docs.microsoft.com/en-us/azure/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

        tạo 1 snapshot, thay đổi 1 block của blob gốc => bị tính phí 4 blocks 1 2 3 4.
    - trường hợp 3:

        ![](https://docs.microsoft.com/en-us/azure/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)
        
        tính phí 8 blocks: 1 2 3 4 5 6 7 8
