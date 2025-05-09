# Crud-App-with-ASP.NET
Webform1.aspx.cs
usingSystem;
usingSystem.Collections.Generic; using System.Linq;
using System.Web; usingSystem.Web.UI;
usingSystem.Web.UI.WebControls; using System.IO;
usingSystem.Drawing;
usingSystem.Data.SqlClient; using System.Configuration; using System.Data;

namespaceCrudApp
{
publicpartialclassWebForm1:System.Web.UI.Page
{
stringcs=ConfigurationManager.ConnectionStrings["dbcs"].ConnectionString; protected void Page_Load(object sender, EventArgs e)
{
if(!IsPostBack)
{
BindGridView();
}
}
voidResetControls()
{
 
"";
 
IDTextBox.Text=NAMETextBox.Text=AGETextBox.Text=SALARYTextBox.Text=
GENDERDropDownList.ClearSelection(); DESIGNATIONDropDownList.ClearSelection(); Label1.Visible = false;
GetImage.Visible = false; GridView1.SelectedIndex=-1;
}
 
protectedvoidINSERTButton_Click(objectsender,EventArgse)
{
SqlConnection con = new SqlConnection(cs); stringfilepath=Server.MapPath("images/");
stringfileName=Path.GetFileName(FileUpload1.FileName); string extension = Path.GetExtension(fileName); HttpPostedFile PostedFile = FileUpload1.PostedFile;
intsize=PostedFile.ContentLength;

if(FileUpload1.HasFile==true)
{
if(extension.ToLower()==".jpg"||extension.ToLower()==".jpeg"|| extension.ToLower() == ".png")
{
if(size<=1000000)
{
string query2 = "select * from emp where id = @id"; SqlCommand cmd2 = new SqlCommand(query2,con); cmd2.Parameters.AddWithValue("@id",IDTextBox.Text); con.Open();
SqlDataReaderdr=cmd2.ExecuteReader(); if (dr.HasRows == true)
{
 

!!')</script>");
 
Response.Write("<script>alert('IdAlreadyExists

con.Close();
}
 
else
{
con.Close();
FileUpload1.SaveAs(filepath+fileName); string path2 = "images/"+ fileName;
stringquery="insertintoemp values(@id,@name,@age,@gender,@desig,@salary,@img)";
SqlCommand cmd = new SqlCommand(query, con); cmd.Parameters.AddWithValue("@id", IDTextBox.Text); cmd.Parameters.AddWithValue("@name",NAMETextBox.Text); cmd.Parameters.AddWithValue("@age", AGETextBox.Text); cmd.Parameters.AddWithValue("@gender",
GENDERDropDownList.SelectedItem.Value);
cmd.Parameters.AddWithValue("@desig", DESIGNATIONDropDownList.SelectedItem.Value);
cmd.Parameters.AddWithValue("@salary",
 
SALARYTextBox.Text);





!!')</script>");
 
cmd.Parameters.AddWithValue("@img",path2); con.Open();
inta=cmd.ExecuteNonQuery(); if (a > 0)
{
Response.Write("<script>alert('InsertedSuccessfully
BindGridView(); ResetControls(); Label1.Visible=false;
}
 
else
{
 
!!')</script>");
 
Response.Write("<script>alert('InsertionFailed

}
 
con.Close();
}
}
else
{
Label1.Text="Lengthshouldbelessthan1MB"; Label1.Visible = true;
Label1.ForeColor=Color.Red;
}
}
else{
Label1.Text="Formatnotsupported!"; Label1.Visible = true;
Label1.ForeColor=Color.Red;
 
}
else
{
 
}



Label1.Text="PleaseUploadanimage"; Label1.Visible = true;
Label1.ForeColor=Color.Red;
 

}
}
 
protectedvoidRESETButton_Click(objectsender,EventArgse)
{
ResetControls();
}
voidBindGridView()
{
SqlConnectioncon=newSqlConnection(cs); string query = "select * from emp";
SqlDataAdaptersda=newSqlDataAdapter(query,con); DataTable data = new DataTable();
sda.Fill(data); GridView1.DataSource=data; GridView1.DataBind();
}
protectedvoidGridView1_SelectedIndexChanged(objectsender,EventArgse)
{
GridViewRowrow=GridView1.SelectedRow;
Label lblId = (Label)row.FindControl("LabelId"); Labellblname=(Label)row.FindControl("LabelName"); Label lblage = (Label)row.FindControl("LabelAge");
Label lblgender = (Label)row.FindControl("LabelGender"); Labellbldesig=(Label)row.FindControl("LabelDesignation"); Label lblsalary = (Label)row.FindControl("LabelSalary"); System.Web.UI.WebControls.Image img =
(System.Web.UI.WebControls.Image)row.FindControl("Image1");
IDTextBox.Text=lblId.Text; NAMETextBox.Text = lblname.Text; AGETextBox.Text = lblage.Text; GENDERDropDownList.Text = lblgender.Text; DESIGNATIONDropDownList.Text=lbldesig.Text; SALARYTextBox.Text = lblsalary.Text; GetImage.ImageUrl = img.ImageUrl; GetImage.Visible = true;
}
protectedvoidUPDATEButton_Click(objectsender,EventArgse)
{
SqlConnection con = new SqlConnection(cs); stringfilepath=Server.MapPath("images/");
stringfileName=Path.GetFileName(FileUpload1.FileName); string extension = Path.GetExtension(fileName); HttpPostedFile PostedFile = FileUpload1.PostedFile;
intsize=PostedFile.ContentLength;
string UpdatePath = "images/"; if(FileUpload1.HasFile==true)
{
if(extension.ToLower()==".jpg"||extension.ToLower()==".jpeg"|| extension.ToLower() == ".png")
{
if(size<=1000000)
{

UpdatePath = UpdatePath + fileName; FileUpload1.SaveAs(Server.MapPath(UpdatePath));
 
string query = "Update emp set name = @name, age = @age, gender=@gender,designation=@desig,salary=@salary,image_path=@imgwhereid= @id";
SqlCommand cmd = new SqlCommand(query,con); cmd.Parameters.AddWithValue("@id", IDTextBox.Text); cmd.Parameters.AddWithValue("@name", NAMETextBox.Text); cmd.Parameters.AddWithValue("@age", AGETextBox.Text); cmd.Parameters.AddWithValue("@gender",
GENDERDropDownList.Text);
cmd.Parameters.AddWithValue("@desig",
DESIGNATIONDropDownList.Text);
cmd.Parameters.AddWithValue("@salary",SALARYTextBox.Text); cmd.Parameters.AddWithValue("@img", UpdatePath); con.Open();
inta=cmd.ExecuteNonQuery(); if(a > 0)
{
 

!!')</script>");






!!')</script>");
 






}
else{

}
 
Response.Write("<script>alert('UpdatedSuccessfully
BindGridView(); ResetControls(); Label1.Visible = false; GetImage.Visible=false;

Response.Write("<script>alert('NotUpdated
 
con.Close();



}
else{
Label1.Text="Lengthshouldbelessthan1MB"; Label1.Visible = true;
Label1.ForeColor=Color.Red;
}
}
else{
Label1.Text="Formatnotsupported!"; Label1.Visible = true;
Label1.ForeColor=Color.Red;
 

}
else
{
 
}



UpdatePath=GetImage.ImageUrl.ToString();
stringquery="Updateempsetname=@name,age=@age,gender=
 
@gender, designation = @desig, salary = @salary, image_path = @img where id = @id"; SqlCommand cmd = new SqlCommand(query, con); cmd.Parameters.AddWithValue("@id", IDTextBox.Text); cmd.Parameters.AddWithValue("@name", NAMETextBox.Text); cmd.Parameters.AddWithValue("@age", AGETextBox.Text); cmd.Parameters.AddWithValue("@gender", GENDERDropDownList.Text); cmd.Parameters.AddWithValue("@desig",DESIGNATIONDropDownList.Text); cmd.Parameters.AddWithValue("@salary", SALARYTextBox.Text); cmd.Parameters.AddWithValue("@img", UpdatePath);
con.Open();
inta=cmd.ExecuteNonQuery(); if (a > 0)
{
 

!!')</script>");
 
Response.Write("<script>alert('UpdatedSuccessfully

BindGridView(); ResetControls(); Label1.Visible = false; GetImage.Visible=false;

stringDeletePath=Server.MapPath(GetImage.ImageUrl.ToString()); if (File.Exists(DeletePath) == true)
{
 
File.Delete(DeletePath);
}
}
else
{
Response.Write("<script>alert('NotUpdated!!')</script>");
}
con.Close();
}
}

protectedvoidDELETEButton_Click(objectsender,EventArgse)
{
SqlConnection con = new SqlConnection(cs); stringquery="deletefromempwhereid=@id"; SqlCommand cmd = new SqlCommand(query, con);
cmd.Parameters.AddWithValue("@id",IDTextBox.Text);
con.Open();
inta=cmd.ExecuteNonQuery(); if (a > 0)
{
Response.Write("<script>alert('DeletedSuccessfully!!')</script>"); BindGridView();
ResetControls(); Label1.Visible = false; GetImage.Visible=false;
stringDeletePath=Server.MapPath(GetImage.ImageUrl.ToString()); if(File.Exists(DeletePath) == true)
{
File.Delete(DeletePath);
}
}
else
{
Response.Write("<script>alert('NotDeleted!!')</script>");
}
con.Close();
}

}


}
Web form1
<%@PageLanguage="C#"AutoEventWireup="true"CodeBehind="WebForm1.aspx.cs"Inherits="CrudApp.WebForm1"%>

<!DOCTYPEhtml>


<htmlxmlns="http://www.w3.org/1999/xhtml">
<headrunat="server">
<title></title>
<styletype="text/css">
.auto-style1 { width:400PX;
border:5pxblackridge; margin:auto;
}
.auto-style2{
}
.auto-style3{
}
.auto-style4 { height:37px;
}
.auto-style5 { height:25px;
}
.auto-style6 { width:80px;
}
.auto-style7 { height:37px; width: 80px;
 
}
.auto-style8 { height:25px; width: 80px;
}
.auto-style9 { width: 80px; height:38px;
}
.auto-style10 { height:38px;
}
</style>
</head>
<body>
<formid="form1"runat="server">
<div>

</div>
<tablecellpadding="4"cellspacing="4"class="auto-style1">
<tr>
<tdclass="auto-style2"colspan="2"><h1style="text- align:center;">EMPLOYEE CRUD APPLICATION</h1></td>
</tr>
<tr>
<tdclass="auto-style6">ID</td>
<td>
<asp:TextBoxID="IDTextBox"runat="server"Height="19px"Width="176px"></asp:TextBox>
<asp:RequiredFieldValidatorID="RequiredFieldValidator2"runat="server"ControlToValidate="IDTextBox"ErrorMessage="Id Required"ForeColor="Green"SetFocusOnError="True">*</asp:RequiredFieldValidator>
</td>
</tr>
<tr>
<tdclass="auto-style7">NAME</td>
<tdclass="auto-style4">
<asp:TextBoxID="NAMETextBox"runat="server"Height="19px"Width="176px"></asp:TextBox>
<asp:RequiredFieldValidatorID="RequiredFieldValidator3"runat="server"ControlToValidate="NAMETextBox"ErrorMessage="Name Required"ForeColor="Green"SetFocusOnError="True">*</asp:RequiredFieldValidator>
</td>
</tr>
<tr>
<tdclass="auto-style6">AGE</td>
<td>
<asp:TextBoxID="AGETextBox"runat="server"Height="19px"Width="176px"></asp:TextBox>
<asp:RequiredFieldValidatorID="RequiredFieldValidator4"runat="server"ControlToValidate="AGETextBox"ErrorMessage="Age Required"ForeColor="Green"SetFocusOnError="True">*</asp:RequiredFieldValidator>
</td>
</tr>
<tr>
<tdclass="auto-style6">GENDER</td>
<td>
<asp:DropDownListID="GENDERDropDownList"runat="server"Height="19px"Width="185px">
<asp:ListItem>SelectGender</asp:ListItem>
<asp:ListItem>Male</asp:ListItem>
<asp:ListItem>Female</asp:ListItem>
 
</asp:DropDownList>
<asp:RequiredFieldValidator ID="RequiredFieldValidator5"runat="server"ControlToValidate="GENDERDropDownList"ErrorMessage="GenderRequired"ForeColor="Green"SetFocusOnError="True"InitialValue="Select Gender">*</asp:RequiredFieldValidator>
</td>
</tr>
<tr>
<tdclass="auto-style9">DESIGNATION</td>
<tdclass="auto-style10">
<asp:DropDownListID="DESIGNATIONDropDownList"runat="server"Height="19px"Width="185px">
<asp:ListItem>Selectdesignation</asp:ListItem>
<asp:ListItem>Manager</asp:ListItem>
<asp:ListItem>AssistantManager</asp:ListItem>
<asp:ListItem>Incharge</asp:ListItem>
<asp:ListItem>Operator</asp:ListItem>
<asp:ListItem>Director</asp:ListItem>
<asp:ListItem>PA</asp:ListItem>
</asp:DropDownList>
<asp:RequiredFieldValidator ID="RequiredFieldValidator6"runat="server"ControlToValidate="DESIGNATIONDropDownList"ErrorMessage="Designation Required"ForeColor="Green"SetFocusOnError="True"InitialValue="Select designation">*</asp:RequiredFieldValidator>
</td>
</tr>
<tr>
<tdclass="auto-style8">SALARY</td>
<tdclass="auto-style5">
<asp:TextBoxID="SALARYTextBox"runat="server"Height="19px"Width="176px"></asp:TextBox>
<asp:RequiredFieldValidator ID="RequiredFieldValidator7"runat="server"ControlToValidate="SALARYTextBox"ErrorMessage="SalaryRequired"ForeColor="Green"SetFocusOnError="True">*</asp:RequiredFieldValidator>
</td>
</tr>
<tr>
<tdclass="auto-style6">IMAGE</td>
<td>
<asp:ImageID="GetImage"Height="70"Width="70"Visible="false"
runat="server"/>
<br/>
<asp:LabelID="Label1"runat="server"Text="Label"
Visible="False"></asp:Label>
<asp:FileUploadID="FileUpload1"runat="server"Width="184px"/>
</td>
</tr>
<tr>
<tdclass="auto-style3"colspan="2">
<asp:ButtonID="INSERTButton"runat="server"Text="INSERT"Width="63px"OnClick="INSERTButton_Click" />
<asp:ButtonID="UPDATEButton"runat="server"Text="UPDATE"Width="63px"OnClick="UPDATEButton_Click" />
<asp:ButtonID="DELETEButton"runat="server"Text="DELETE"Width="63px"OnClick="DELETEButton_Click" />
<asp:ButtonID="RESETButton"runat="server"Text="RESET"Width="63px"OnClick="RESETButton_Click" />
</td>
</tr>
<tr>
<tdclass="auto-style3"colspan="2">
 
<asp:ValidationSummaryID="ValidationSummary1"runat="server"BorderColor="Silver"ForeColor="#339933" />
</td>
</tr>
</table>
<br/>
<asp:GridViewID="GridView1"runat="server"AutoGenerateColumns="False"BackColor="White"BorderColor="#999999"BorderStyle="None"BorderWidth="1px"CellPadding="3"GridLines="Vertical"HorizontalAlign="Center"OnSelectedIndexChanged="GridView1_SelectedIndexChanged">
<AlternatingRowStyleBackColor="#DCDCDC"/>
<Columns>
<asp:CommandFieldShowSelectButton="True"/>
<asp:TemplateFieldHeaderText="ID">
<ItemTemplate>
<asp:LabelID="LabelId"runat="server"Text='<%#Eval("id")
%>'>'></asp:Label>

</ItemTemplate>
</asp:TemplateField>
<asp:TemplateFieldHeaderText="NAME">
<ItemTemplate>
<asp:LabelID="LabelName"runat="server"Text='<%# Eval("name") %>'>'></asp:Label>
</ItemTemplate>
</asp:TemplateField>
<asp:TemplateFieldHeaderText="AGE">
<ItemTemplate>
<asp:LabelID="LabelAge"runat="server"Text='<%#Eval("age")
%>'>'></asp:Label>
</ItemTemplate>
</asp:TemplateField>
<asp:TemplateFieldHeaderText="GENDER">
<ItemTemplate>
<asp:LabelID="LabelGender"runat="server"Text='<%# Eval("gender") %>'>'></asp:Label>
</ItemTemplate>
</asp:TemplateField>
<asp:TemplateFieldHeaderText="DESIGNATION">
<ItemTemplate>
<asp:LabelID="LabelDesignation"runat="server"Text='<%# Eval("designation") %>'>'></asp:Label>

</ItemTemplate>
</asp:TemplateField>
<asp:TemplateFieldHeaderText="SALARY">
<ItemTemplate>
<asp:LabelID="LabelSalary"runat="server"Text='<%# Eval("salary") %>'>'></asp:Label>

</ItemTemplate>
</asp:TemplateField>
<asp:TemplateFieldHeaderText="IMAGE">
<ItemTemplate>
<asp:ImageID="Image1"Height="100"Width="100"ImageUrl='<%# Eval("image_path") %>'runat="server" />
</ItemTemplate>
</asp:TemplateField>
 
</Columns>
<FooterStyleBackColor="#CCCCCC"ForeColor="Black"/>
<HeaderStyleBackColor="#000084"Font-Bold="True"ForeColor="White"/>
<PagerStyleBackColor="#999999"ForeColor="Black"HorizontalAlign="Center"
/>
<RowStyleBackColor="#EEEEEE"ForeColor="Black"/>
<SelectedRowStyleBackColor="#008A8C"Font-Bold="True"ForeColor="White"
/>
<SortedAscendingCellStyleBackColor="#F1F1F1"/>
<SortedAscendingHeaderStyleBackColor="#0000A9"/>
<SortedDescendingCellStyleBackColor="#CAC9C9"/>
<SortedDescendingHeaderStyleBackColor="#000065"/>
</asp:GridView>

</form>
</body>
</html>

