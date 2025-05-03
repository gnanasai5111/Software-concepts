## Route Handlers
- Route Handlers  are used to define custom API endpoints directly inside the app/ directory using the App Router.
- You create them using special files like route.ts or route.js:

**Folder Structure**
```
app/
 comments/
   route.ts         ← handles GET and POST
   [id]/
     route.ts       ← Handles `GET`, `PATCH`, and `DELETE` for specific comment
   comments.ts      ← contains comments data
```

**comments.ts**
```
export const comments = [
  { id: 1, text: "Good doing" },
  { id: 2, text: "Excellent Work" },
  { id: 3, text: "Fantastic" },
];
```

**GET , POST Requests**
```
import { comments } from "./comments";

// GET - Fetch all comments
export async function GET() {
  return Response.json(comments);
}

// POST - Add a new comment
export async function POST(request: Request) {
  const body = await request.json();
  const newComment = {
    id: Date.now(),
    ...body,
  };

  comments.push(newComment);
  return new Response(
    JSON.stringify({ message: "Comment Added Succesfully!", ...newComment }),
    { headers: { "Content-Type": "application/json" }, status: 201 }
  );
}
```

**Handles GET, PATCH, and DELETE for specific comment(`/comments/[id]/route.ts`)**
```
import { comments } from "../comments";

// GET - Fetch a single comment by ID
export async function GET(
  _request: Request,
  { params }: { params: Promise<{ id: string }> }
) {
  const { id } = await params;

  const comment = comments.find((comment) => comment.id === parseInt(id));

  if (!comment) {
    return Response.json({ message: "Comment not found" }, { status: 404 });
  }

  return Response.json(comment);
}

// PATCH - Update a comment's text by ID
export async function PATCH(
  request: Request,
  { params }: { params: Promise<{ id: string }> }
) {
  const { id } = await params;
  const { text } = await request.json();

  const index = comments.findIndex((comment) => comment.id === parseInt(id));
  if (index === -1) {
    return Response.json({ message: "Comment not found" }, { status: 404 });
  }

  comments[index].text = text;
  return Response.json({ message: "Updated Successfully", ...comments[index] });
}

// DELETE - Delete a comment by ID
export async function DELETE(
  _request: Request,
  { params }: { params: Promise<{ id: string }> }
) {
  const { id } = await params;

  const index = comments.findIndex((comment) => comment.id === parseInt(id));

  if (index === -1) {
    return Response.json({ message: "Comment not found" }, { status: 404 });
  }

  const deletedComment = comments[index];
  comments.splice(index, 1);

  return Response.json({ message: "Deleted Successfully", ...deletedComment });
}
```

**Query Params**
```

// GET Handler for fetching comments.
// If a query params `id` is present (`/comments?id=1`), it will return the comment with that specific ID.
// If no `id` is provided, it will return the full list of comments.
export async function GET(request: Request) {
  const url = new URL(request.url);
  const id = url.searchParams.get("id");

  if (id) {
    const comment = comments.find((comment) => comment.id === parseInt(id));
    if (!comment) {
      return Response.json({ message: "Comment not found" }, { status: 404 });
    }

    return Response.json(comment);
  }
  return Response.json(comments);
}

// Alternative way
import { NextRequest } from "next/server";
import { comments } from "./comments";

export async function GET(request: NextRequest) {
  const id = request.nextUrl.searchParams.get("id");

  if (id) {
    const comment = comments.find((comment) => comment.id === parseInt(id));
    if (!comment) {
      return Response.json({ message: "Comment not found" }, { status: 404 });
    }

    return Response.json(comment);
  }
  return Response.json(comments);
}

```


**Accessing Request Headers**
```
export async function GET(request: Request) {
    const headers = request.headers;
  
    const userAgent = headers.get("user-agent");
    const Authorization= headers.get("Authorization");
  
    return Response.json({ userAgent, Authorization });
}

// Alternative way
import { NextRequest } from "next/server";

export async function GET(request: NextRequest) {
    const headers = new Headers(request.headers);
  
    const userAgent = headers.get("user-agent");
    const Authorization= headers.get("Authorization");
  
    return Response.json({ userAgent, Authorization });
}
```

**sending headers in the response**
```
  return new Response(
  JSON.stringify(data), // ensure the body is a string
  {
    headers: { "Content-Type": "application/json" },
    status: 201,
  }
);
```

**accessing and setting cookie**
```
import { NextRequest } from "next/server";

export async function GET(request: NextRequest) {
  const theme = request.cookies.get("theme");
  console.log(theme);
  return new Response("hello", {
    headers: {
      "Content-Type": "application/json",
      "Set-Cookie": "theme=dark",
    },
  });
}
```

**redirect**
```
import { redirect } from "next/navigation";

export async function GET() {
  // This will redirect to /login
  redirect("/login");
}
```
