const WEBAPP_TITLE = "อัลบั้มภาพ ITCom7-Onsite Event"; // ชื่อหลักของเว็บแอปพลิเคชัน ใช้แสดงบนแท็บเบราว์เซอร์และใน Header
const WEBAPP_INDEXTITLE = "อัลบั้มภาพ ITCom7-Onsite Event"; // เว็บแอปพลิเคชัน navbar-title
const FAVICON_URL = "https://img2.pic.in.th/pic/60bc7192ac918d169457719850927ef6.png"; // URL ของรูปภาพ ไอคอนที่จะแสดงบนแท็บเบราว์เซอร์ (Favicon) และ logo เว็บ
const WEBAPP_SUBTITLE = "ITCom7-Onsite Event ©2025 All rights reserved"; // ชื่อหลักของเว็บแอปพลิเคชัน ใช้แสดงบนแท็บเบราว์เซอร์และใน footer
const mainFolderId = "1SQ06SG7PlOSKNDobpSF4b47JWjH7f74F"; //ID ของโฟลเดอร์หลักใน Google Drive ที่เก็บอัลบั้มทั้งหมด

const SCRIPT_NAME = "อัลบั้มภาพ logger"; // Logger สำหรับการตรวจสอบการทำงาน
function logger(message, data = "") {
  console.log(`${SCRIPT_NAME}: ${message}`, data);
}
/**
* ฟังก์ชันสำหรับดึงชื่อโฟลเดอร์โดยใช้ระบบ Cache
* @param {string} folderId รหัสของโฟลเดอร์ Google Drive
* @return {string} ชื่อโฟลเดอร์
*/
function getFolderName(folderId) {
  const cache = CacheService.getScriptCache();
  const cacheKey = 'folderName_v1_' + folderId;

  const cachedName = cache.get(cacheKey);
  if (cachedName) {
    return cachedName;
  }

  const folderName = DriveApp.getFolderById(folderId).getName();
  // เก็บชื่อโฟลเดอร์ไว้ใน Cache 6 ชั่วโมง (ชื่อโฟลเดอร์ไม่ค่อยเปลี่ยน)
  cache.put(cacheKey, folderName, 21600); 
  return folderName;
}

function doGet(e) {
  // ตรวจสอบ URL: ถ้าเป็นหน้าอัลบั้ม
  if (e && e.parameter && e.parameter.page === "album" && e.parameter.folderId) {
    const folderId = e.parameter.folderId;
    try {
      const folderName = getFolderName(folderId);
      const template = HtmlService.createTemplateFromFile("Album");
      template.folderId = folderId;
      template.folderName = folderName;
      template.pagenavbartitle = WEBAPP_INDEXTITLE;
      template.pageSubtitle = WEBAPP_SUBTITLE;

      return template
        .evaluate()
        .setTitle(folderName)
        .setFaviconUrl(FAVICON_URL)
        .addMetaTag("viewport", "width=device-width, initial-scale=1.0")
        .setSandboxMode(HtmlService.SandboxMode.IFRAME);
    } catch (err) {
      logger("เกิดข้อผิดพลาดในการเปิดอัลบั้ม (folderId: " + folderId + ")", err.toString());
      
      // ---- แก้ไขส่วนนี้ ----
      // 1. สร้าง template และส่งตัวแปรไปก่อน
      const template = HtmlService.createTemplateFromFile("Index");
      template.pageTitle = WEBAPP_TITLE;
      template.pagenavbartitle = WEBAPP_INDEXTITLE;
      template.pageSubtitle = WEBAPP_SUBTITLE;
      
      // 2. ค่อย return ผลลัพธ์สุดท้าย
      return template.evaluate()
        .setTitle("Photo Album - ไม่พบอัลบั้ม")
        .setFaviconUrl(FAVICON_URL)
        .addMetaTag("viewport", "width=device-width, initial-scale=1.0")
        .setSandboxMode(HtmlService.SandboxMode.IFRAME);
    }
  } else {
    // ---- แก้ไขส่วนนี้ ----
    // 1. สร้าง template และส่งตัวแปรไปก่อน
    const template = HtmlService.createTemplateFromFile("Index");
    template.pageTitle = WEBAPP_TITLE;
    template.pagenavbartitle = WEBAPP_INDEXTITLE;
    template.pageSubtitle = WEBAPP_SUBTITLE;

    // 2. ค่อย return ผลลัพธ์สุดท้าย
    return template
      .evaluate()
      .setTitle(WEBAPP_TITLE)
      .setFaviconUrl(FAVICON_URL)
      .addMetaTag("viewport", "width=device-width, initial-scale=1.0")
      .setSandboxMode(HtmlService.SandboxMode.IFRAME);
  }
}

function getAlbumData() {
  const cache = CacheService.getScriptCache();
  const cacheKey = 'albumData_v3'; // เปลี่ยน v2 เป็น v3 เพื่อบังคับให้โหลดข้อมูลใหม่
  const cachedData = cache.get(cacheKey);
  if (cachedData) {
    logger("ดึงข้อมูลอัลบั้มจาก cache สำเร็จแล้ว");
    return JSON.parse(cachedData);
  }

  logger("แคชหายไป กำลังดึงข้อมูลอัลบั้มจาก Google Drive...");
  try {
    const mainFolder = DriveApp.getFolderById(mainFolderId);
    const subFolders = mainFolder.getFolders();
    const albums = [];
    let totalFilesCount = 0;
    let grandTotalSize = 0; // << เพิ่ม: ตัวแปรสำหรับเก็บขนาดไฟล์รวมทั้งหมด

    while (subFolders.hasNext()) {
      const folder = subFolders.next();
      const files = folder.getFiles();
      let fileCountInFolder = 0;
      let totalSizeInFolder = 0;
      let thumbnailUrl = null;

      while (files.hasNext()) {
        const file = files.next();
        if (fileCountInFolder === 0) {
          thumbnailUrl = `https://lh3.googleusercontent.com/d/${file.getId()}`;
        }
        fileCountInFolder++;
        totalSizeInFolder += file.getSize();
      }

      if (fileCountInFolder > 0) {
        grandTotalSize += totalSizeInFolder; // << เพิ่ม: นำขนาดของแต่ละโฟลเดอร์มารวมกัน
        totalFilesCount += fileCountInFolder;
        
        const webAppUrl = ScriptApp.getService().getUrl();
        const folderId = folder.getId();
        const albumWebAppUrl = `${webAppUrl}?page=album&folderId=${folderId}&openExternalBrowser=1`;

        albums.push({
          id: folderId,
          name: folder.getName(),
          fileCount: fileCountInFolder,
          totalSizeMB: (totalSizeInFolder / (1024 * 1024)).toFixed(2),
          shareLink: albumWebAppUrl,
          thumbnailUrl: thumbnailUrl
        });
      }
    }

    // << เพิ่ม: ส่วนแปลงหน่วย MB/GB อัตโนมัติ
    let totalSizeFormatted;
    const totalSizeMB = grandTotalSize / (1024 * 1024);
    if (totalSizeMB >= 1024) {
      const totalSizeGB = totalSizeMB / 1024;
      totalSizeFormatted = `${totalSizeGB.toFixed(2)} GB`;
    } else {
      totalSizeFormatted = `${totalSizeMB.toFixed(2)} MB`;
    }

    const albumData = {
      totalAlbums: albums.length,
      totalFiles: totalFilesCount,
      totalStorageUsed: totalSizeFormatted, // << เพิ่ม: property ใหม่สำหรับขนาดไฟล์รวม
      albums: albums,
    };

    cache.put(cacheKey, JSON.stringify(albumData), 7200);
    logger("ข้อมูลอัลบั้มดึงมาจาก Google Drive และเก็บไว้ใน cache");
    return albumData;

  } catch (e) {
    logger("เกิดข้อผิดพลาดในการดึงข้อมูลอัลบั้ม", e.toString());
    return { error: e.toString() };
  }
}

function getImagesInAlbum(folderId) {
  const cache = CacheService.getScriptCache();
  const cacheKey = 'imagesInAlbum_v1_' + folderId; // สร้าง Key สำหรับแต่ละอัลบั้ม

  // 1. ตรวจสอบข้อมูลจาก Cache ก่อน
  const cachedImages = cache.get(cacheKey);
  if (cachedImages) {
    logger(`ดึงรูปภาพสำหรับโฟลเดอร์ ${folderId} จาก cache`);
    return JSON.parse(cachedImages);
  }

  // 2. ถ้าไม่มีใน Cache ให้ไปดึงข้อมูลจาก Drive (แบบเดิม)
  logger(`cache หายไป กำลังดึงรูปภาพสำหรับโฟลเดอร์ ${folderId} จาก Google Drive`);
  try {
    const folder = DriveApp.getFolderById(folderId);
    const files = folder.getFiles();
    const images = [];
    while (files.hasNext()) {
      const file = files.next();
      const imageUrl = `https://lh3.googleusercontent.com/d/${file.getId()}`;
      images.push({
        id: file.getId(),
        name: file.getName(),
        url: imageUrl,
        downloadUrl: file.getDownloadUrl(),
      });
    }

    // 3. จัดเก็บข้อมูลใหม่ลง Cache ก่อนส่งกลับไป (เก็บไว้ 2 ชั่วโมง)
    try {
      cache.put(cacheKey, JSON.stringify(images), 7200);
      logger(`ดึงรูปภาพจากโฟลเดอร์ ${folderId} และเก็บไว้ใน cache`);
      
    } catch (cacheErr) {
      logger(`ไม่สามารถ cache รูปภาพสำหรับโฟลเดอร์ ${folderId} ได้ ขนาดข้อมูลอาจใหญ่เกินไป`, cacheErr.toString());
      
    }
    
    return images;

  } catch (e) {
    logger(`เกิดข้อผิดพลาดในการดึงรูปภาพสำหรับโฟลเดอร์ ${folderId}`, e.toString());
    return { error: e.toString() };
  }
}

// Function สำหรับ include ไฟล์อื่นเข้ามาใน HTML
function include(filename) {
  return HtmlService.createHtmlOutputFromFile(filename).getContent();
}

/**
 * ฟังก์ชันสำหรับเคลียร์ Cache ของข้อมูลอัลบั้มด้วยตนเอง
 * ใช้ในกรณีที่ต้องการอัปเดตข้อมูลทันที
 */
function clearAlbumCache() {
  const cache = CacheService.getScriptCache();
  const cacheKey = 'albumData_v1';
  cache.remove(cacheKey);
  logger('แคชข้อมูลอัลบั้มถูกล้างแล้ว!');
}
