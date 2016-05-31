#Spring boot
1. Create pesertaDaoTest.
2. Auto-matic Testing Junit.
	- Test Annotation.
	- After and Before Annotation.
3. create data resources "entity.sql"
4. Execute sql before @Test.

##Code
	1. Create pesertaDaoTest with JUnit.
		@Autowired
		private PesertaDao pd;
		@Autowired
		private DataSource dataSource;
		
		//hapus
			@After
			public void hapusData() throws SQLException{
				String sql = "delete from peserta where email = 'arrizaqu@yahoo.com'";
				try(Connection c = dataSource.getConnection()){
					c.createStatement().executeUpdate(sql);
				}
			}
		
		@Test
		public void testInsert() throws SQLException{
			Peserta peserta = new Peserta();
			peserta.setName("masyda arrizaqu");
			peserta.setEmail("arrizaqu@yahoo.com");
			peserta.setTanggalLahir(new Date());
		
			pd.save(peserta);
			
			//selec data for test
			String sql = "select count(*) as jumlah from peserta where email = 'arrizaqu@yahoo.com'";
			
			Connection con = null;
			con = dataSource.getConnection();
			
			ResultSet rs = con.createStatement().executeQuery(sql);
			Assert.assertTrue(rs.next());
			Long jumlaRow = rs.getLong("jumlah");
			Assert.assertEquals(1L, jumlaRow.longValue());
			
			con.close();
			
		}
		
		//untuk mengetes apakah data ada dalam jumlah tertentu
		@Test 
		public void hitung(){
			Long jumlah = pd.count();
			Assert.assertEquals(3L, jumlah.longValue());
		}
		
		//untuk mengetes apakah data ada dalam dengan ID tertentu
		@Test
		public void testCariById(){
			Peserta p = pd.findOne("aa1");
			Assert.assertNotNull(p);
			Assert.assertEquals("peserta test 001 ", p.getName());
			
			// cari jika tidak ada
			Peserta px = pd.findOne("xx");
			Assert.assertNull(px);
		}
		
	3. create data resources "entity.sql"
		delete from peserta;
		insert into peserta(id, name, email, tanggal_lahir)
		value('aa1', 'peserta test 001 ', 'peserta.test.001@gmail.com', '2011-01-01');

		insert into peserta(id, name, email, tanggal_lahir)
		value('aa2', 'peserta test 002 ', 'peserta.test.002@gmail.com', '2011-01-02');

		insert into peserta(id, name, email, tanggal_lahir)
		value('aa3', 'peserta test 003 ', 'peserta.test.003@gmail.com', '2011-01-03');

	4. Execute sql before @Test.
		@Sql(executionPhase =ExecutionPhase.BEFORE_TEST_METHOD,
		scripts = "/data/peserta.sql"
			)
##Reference


