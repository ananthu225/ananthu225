const { kurukkan, mode ,sendMenu, sendSegMenu, setMenuType } = require("../lib/");
kurukkan({
    pattern: "menu ?(.*)",
    desc: "kurukkan user manual",
    fromMe: mode,
    type: "user",
}, async (message, match) => {
    await sendMenu(message, match);
});
kurukkan({
    pattern: "setmenu ?(.*)",
    desc: "kurukkan menu control panel",
    fromMe: true,
    type: "user",
}, async (message, match) => {
    await setMenuType(message, match);
});
const pluginTypes = ['AnimeImage', 'downloader', 'info', 'whatsapp', 'group', 'media', 'AnimeVideo', 'user', 'generator'];

pluginTypes.forEach((type) => {
kurukkan({
        pattern: `.${type}$`,
        fromMe: mode,
        dontAddCommandList: true,
    }, async (message, match) => {
        await sendSegMenu(message, match,type);
    });
});
