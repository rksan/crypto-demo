<template src="./template.html"></template>
<style scoped src="./styles.css"></style>

<script>
import { computed, defineComponent, reactive } from "vue";

const { Buffer } = require("buffer");
const crypto = require("crypto");

const setup = () => {
  const algorithms = crypto.getCiphers();

  const encodings = [
    "ascii",
    "utf8",
    "utf16le",
    "ucs2",
    "base64",
    "binary",
    "hex",
  ];

  // $data
  const model = {
    algorithms,
    encodings,
    formData: reactive({
      algorithm: algorithms[0],
      password: "",
      plainText: {
        data: "",
        encode: "utf8",
        error: "",
      },
      encrypted: {
        data: "",
        encode: "base64",
        error: "",
      },
    }),
  };

  const compDataSize = computed(() => {
    return (text) => Buffer.byteLength(text.data, text.encode);
  });

  // $methods
  const doRandomPassword = () => {
    model.formData.password = Math.random().toString(36).slice(2);
  };

  const doEncryption = (event) => {
    if (event) {
      event.preventDefault();
      event.stopPropagation();
    }

    const form = document.querySelector("form");

    if (form) {
      if (!form.checkValidity()) {
        form.classList.add("was-validated");
        return false;
      }
    }

    const algorithm = model.formData.algorithm;
    const password = model.formData.password;
    const plainText = {
      data: model.formData.plainText.data,
      encode: model.formData.plainText.encode,
    };
    const encrypted = {
      data: "",
      encode: model.formData.encrypted.encode,
    };

    try {
      const cipher = crypto.createCipher(algorithm, password);
      const buffer = Buffer.from(plainText.data, plainText.encode);

      let data = cipher.update(buffer, plainText.encode, encrypted.encode);
      data += cipher.final(encrypted.encode);

      model.formData.encrypted.data = data;
      model.formData.plainText.error = "";
    } catch (err) {
      model.formData.plainText.error = err;
      console.error(err);
    }
  };

  const doDecryption = (event) => {
    if (event) {
      event.preventDefault();
      event.stopPropagation();
    }

    const form = document.querySelector("form");

    if (form) {
      if (!form.checkValidity()) {
        return false;
      }
    }

    const algorithm = model.formData.algorithm;
    const password = model.formData.password;
    const encrypted = {
      data: model.formData.encrypted.data,
      encode: model.formData.encrypted.encode,
    };
    const plainText = {
      data: "",
      encode: model.formData.plainText.encode,
    };

    try {
      const decipher = crypto.createDecipher(algorithm, password);
      const buffer = Buffer.from(encrypted.data, encrypted.encode);

      let data = decipher.update(buffer, encrypted.encode, plainText.encode);
      data += decipher.final(plainText.encode);

      model.formData.plainText.data = data;
      model.formData.encrypted.error = "";
    } catch (err) {
      model.formData.encrypted.error = err;
      console.error(err);
    }
  };

  const doClearPlainText = (event) => {
    if (event) {
      event.preventDefault();
      event.stopPropagation();
    }

    model.formData.plainText.data = "";
    model.formData.plainText.error = "";
  };

  const doChangeEncryptedEncode = () => {
    model.formData.encrypted.data = "";
    model.formData.encrypted.error = "";
  };

  return {
    model,
    compDataSize,
    doRandomPassword,
    doEncryption,
    doDecryption,
    doClearPlainText,
    doChangeEncryptedEncode,
  };
};

export default defineComponent({
  name: "o-crypto-form",
  setup,
});
</script>
