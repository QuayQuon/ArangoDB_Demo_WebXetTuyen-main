FOR form IN FormXetTuyen
  // tìm các ngành học liên kết với form này
  FOR edge IN FormXetTuyen_NganhHoc
    FILTER edge._from == form._id
    FOR nganh IN NganhHoc
      FILTER nganh._id == edge._to
      RETURN {
        form: form,
        nganh: nganh,
        edge: edge
      }
//
FOR form IN FormXetTuyen
  FOR nganh IN OUTBOUND form FormXetTuyen_NganhHoc
    RETURN {
      form: form,
      nganh: nganh
    }
//
FOR f IN FormXetTuyen_NganhHoc
  FILTER f._from == "FormXetTuyen/999999"
  FOR n IN NganhHoc
    FILTER n._id == f._to
    RETURN {
      tenNganh: n.TenNganhHoc, 
      nganhId: n._id
    }
//lấy ngành theo form
FOR form IN FormXetTuyen
  FOR nganh IN OUTBOUND form FormXetTuyen_NganhHoc
    RETURN {
      form: form,
      nganh: nganh.TenNganhHoc
    }