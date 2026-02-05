<template>
  <div class="container mt-4">
    <h2 class="text-center mb-4">LAB 6 – VueJS</h2>

    <!-- ===== BÀI 1 ===== -->
    <div class="card mb-4">
      <div class="card-header bg-primary text-white">
        Bài 1: Xếp loại học sinh
      </div>
      <div class="card-body">
        <input type="number" class="form-control mb-2" v-model="dtb" placeholder="Nhập điểm trung bình">

        <p v-if="dtb < 5">Xếp loại: Yếu</p>
        <p v-else-if="dtb < 6.5">Xếp loại: Trung bình</p>
        <p v-else-if="dtb < 8">Xếp loại: Khá</p>
        <p v-else-if="dtb < 9">Xếp loại: Giỏi</p>
        <p v-else>Xếp loại: Xuất sắc</p>
      </div>
    </div>

    <!-- ===== BÀI 2 ===== -->
    <div class="card mb-4">
      <div class="card-header bg-success text-white">
        Bài 2: Xác định mùa
      </div>
      <div class="card-body">
        <input type="number" class="form-control mb-2" v-model="thang" placeholder="Nhập tháng">

        <p v-if="thang < 1 || thang > 12" class="text-danger">
          Vui lòng nhập tháng từ 1 đến 12!
        </p>
        <p v-else-if="thang >= 3 && thang <= 5">Mùa Xuân</p>
        <p v-else-if="thang >= 6 && thang <= 8">Mùa Hạ</p>
        <p v-else-if="thang >= 9 && thang <= 11">Mùa Thu</p>
        <p v-else>Mùa Đông</p>
      </div>
    </div>

    <!-- ===== BÀI 3 ===== -->
    <div class="card mb-4">
      <div class="card-header bg-warning">
        Bài 3: Danh sách bài viết
      </div>
      <div class="card-body">
        <div class="row">
          <div class="col-md-4 mb-3" v-for="post in posts" :key="post.id">
            <div class="card h-100">
              <img :src="post.image" class="card-img-top">
              <div class="card-body">
                <h5>{{ post.title }}</h5>
                <p>{{ post.content }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== BÀI 4 ===== -->
    <div class="card mb-4">
      <div class="card-header bg-info text-white">
        Bài 4: CRUD học sinh
      </div>
      <div class="card-body">

        <form @submit.prevent="submitForm">
          <div class="mb-2">
            <label>Họ tên</label>
            <input class="form-control" v-model="student.name" required>
          </div>

          <div class="mb-2">
            <label>Điểm</label>
            <input type="number" class="form-control" v-model="student.score" required>
          </div>

          <div class="mb-2">
            <label>Ngày sinh</label>
            <input type="date" class="form-control" v-model="student.dob" required>
          </div>

          <button class="btn btn-primary mt-2" v-if="editIndex === -1">Thêm</button>
          <button class="btn btn-warning mt-2" v-else>Cập nhật</button>
        </form>

        <table class="table table-bordered mt-4">
          <thead class="table-dark">
            <tr>
              <th>Họ tên</th>
              <th>Điểm</th>
              <th>Ngày sinh</th>
              <th>Hành động</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(s, i) in students" :key="i">
              <td>{{ s.name }}</td>
              <td>{{ s.score }}</td>
              <td>{{ s.dob }}</td>
              <td>
                <button class="btn btn-warning btn-sm me-1" @click="editStudent(i)">Sửa</button>
                <button class="btn btn-danger btn-sm" @click="deleteStudent(i)">Xóa</button>
              </td>
            </tr>
          </tbody>
        </table>

      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      dtb: 0,
      thang: 1,

      posts: [
        { id: 1, title: 'Bài viết 1', content: 'Mô tả bài viết 1', image: 'https://picsum.photos/300/200?1' },
        { id: 2, title: 'Bài viết 2', content: 'Mô tả bài viết 2', image: 'https://picsum.photos/300/200?2' },
        { id: 3, title: 'Bài viết 3', content: 'Mô tả bài viết 3', image: 'https://picsum.photos/300/200?3' }
      ],

      students: [],
      student: { name: '', score: '', dob: '' },
      editIndex: -1
    }
  },
  methods: {
    submitForm() {
      if (this.editIndex === -1) {
        this.students.push({ ...this.student })
      } else {
        this.students[this.editIndex] = { ...this.student }
        this.editIndex = -1
      }
      this.student = { name: '', score: '', dob: '' }
    },
    editStudent(i) {
      this.student = { ...this.students[i] }
      this.editIndex = i
    },
    deleteStudent(i) {
      if (confirm('Bạn có chắc muốn xóa?')) {
        this.students.splice(i, 1)
      }
    }
  }
}
</script>
